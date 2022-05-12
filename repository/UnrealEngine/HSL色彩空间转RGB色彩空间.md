# HSL 色彩空间转 RGB 色彩空间

---



## 转换算法&步骤

1. 根据 L 分量和 S 分量的值计算出中间变量, 记为 Q
    - L < 0.5
        
        Q = L * (1 + S)
        
    - L ≥ 0.5
        
        Q = L + S - (L * S)
        
2. 根据 Q 计算出中间变量, 记为 P
    
    P = 2 * L - Q
    
3. 将 [0, 360] 范围内的 H 分量值转换为 [0, 1] 范围内, 记为 Hk
    
    Hk = H / 360
    
4. 使用 Hk 计算出 R, G, B 三个分量的偏差值, 分辨记为 tR, tG, tB
    
    tR = Hk + 1/3
    
    tG = Hk
    
    tB = Hk - 1/3
    
5. 对上述三个偏差值均执行以下操作, 以下操作中该偏差值记为 tColor, 得到 R, G, B 三个分量的值

    1. 将 tColor 进行范围缩限

        - tColor < 0
            
            tColor = tColor + 1
            
        - tColor > 1
            
            tColor = tColor - 1
            
    2. 使用缩限后的 tColor 计算 R, G, B 通道的分量值, 记为 Color , 取值范围 [0, 1], 可用其转换为 [0, 255] 范围的分量值

        - tColor < 1/6
            
            Color = P + (Q - P) * 6 * tColor
            
        - tColor ≥ 1/6 且 tColor < 0.5
            
            Color = Q
            
        - tColor ≥ 0.5 且 tColor < 2/3
            
            Color = P + (Q - P) * (4 - 6 * tColor)
            
        - tColor ≥ 2/3
            
            Color = P

## 算法代码实现

### JavaScript

```js
const HSLtoRGB = (H, S, L) => {
    const Q = L < 0.5
        ? L * (1 + S)
        : L + S - (L * S)
    const P = 2 * L - Q
    const Hk = H / 360
    const tR = Hk + 1 / 3
    const tG = Hk
    const tB = Hk - 1 / 3

    let R = 0
    let G = 0
    let B = 0
    const t = [tR, tG, tB]
    for (let i = 0; i < t.length; i++) {
        let tColor = t[i]
        if (tColor < 0) {
            tColor += 1
        }
        if (tColor > 1) {
            tColor -= 1
        }
        if (tColor < 1 / 6) {
            tColor = P + (Q - P) * 6 * tColor;
        } else if (tColor >= 1 / 6 && tColor < 0.5) {
            tColor = Q
        } else if (tColor >= 0.5 && tColor < 2 / 3) {
            tColor = P + (Q - P) * (4 - 6 * tColor)
        } else {
            tColor = P
        }
        t[i] = Math.round(tColor * 255)
    }
    [R, G, B] = t
    return { R, G, B }
}
```

### HLSL

```hlsl
float h_value = HSL.x;
float s_value = HSL.y;
float l_value = HSL.z;
float q_value = l_value < 0.5 ? l_value * (1+s_value) : l_value + s_value - (l_value * s_value);
float p_value = 2 * l_value - q_value;
float hk = h_value / 360;
float RGB[] = {(hk+1.0/3.0), hk, (hk-1.0/3.0)};
for(int i=0; i<3;i++){
    float t = RGB[i];
    if(t<0){
        t+=1;
    }
    if(t>1){
        t-=1;
    }
    if (t < 1.0 / 6.0) {
        t = p_value + (p_value - p_value) * 6 * t;
    } else if (t >= 1.0 / 6.0 && t < 0.5) {
        t = q_value;
    } else if (t >= 0.5 && t < 2.0 / 3.0) {
        t = p_value + (q_value - p_value) * (4 - 6 * t);
    } else {
        t = p_value;
    }
   RGB[i] = t;
}
return float3(RGB[0],RGB[1],RGB[2]);
```