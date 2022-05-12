# RGB 色彩空间转 HSL 色彩空间

---



## 转换算法&步骤

1. 如果输入的RGB色彩各通道的取值范围在 [0, 255] 范围内, 则将 R, G, B 三个通道的分量数值转换到 [0, 1] 区间内, 记为 R’, G’, B’

2. 获取 R’, G’, B’ 中的最大值记为 MAX, 最小值记为 MIN

3. 计算 MAX 和 MIN 的差值, 记为 DELTA

4. 计算 L 分量值
    
    L = (MAX+MIN)/2
    
5. 计算 S 分量值

    - MAX = MIN 或 L =0:
        
        S = 0
        
    - L > 0 且 L ≤ 0.5
        
        S = (MAX-MIN)/（MAX+MIN）
        
    - L > 0.5
        
        S = (MAX-MIN)/(2-MAX-MIN)
        
6. 计算 H 分量值

    - MAX = MIN
        
        H = 0
        
    - MAX = R’ 且 G’ ≥ B’
        
        H = 60*(G'-B')/(MAX-MIN)
        
    - MAX = R’ 且 G’ < B’
        
        H = 60*(G'-B')/(MAX-MIN)+360
        
    - MAX = G’
        
        H = 60*(B' -R')/(MAX-MIN)+120
        
    - MAX = B’
        
        H = 60*(R' - G')/(MAX-MIN)+240

## 算法代码实现

### JavaScript

```js
const RGBtoHSL = (R, G, B) => {
    // 1
    const r = R > 1 ? R / 255 : R
    const g = G > 1 ? G / 255 : G
    const b = B > 1 ? B / 255 : B
    // 2
    const MAX = Math.max(r, g, b)
    const MIN = Math.min(r, g, b)
    // 3
    const DELTA = MAX - MIN
    // 4
    const L = ((MAX + MIN) / 2).toFixed(3)
    // 5
    const S = MAX === MIN || L === 0
        ? 0
        : L > 0 && L <= 0.5
            ? ((MAX - MIN) / (MAX + MIN)).toFixed(3)
            : ((MAX - MIN) / (2 - MAX - MIN)).toFixed(3)
    // 6
    const H = MAX === MIN
        ? 0
        : MAX === r && g>=b
            ? (60*(g-b)/(MAX-MIN)).toFixed(3)
            : MAX === r && g<b
                ? (60*(g-b)/(MAX-MIN)+360).toFixed(3)
                : MAX === g
                    ? (60*(g-r)/(MAX-MIN)+120).toFixed(3)
                    : (60*(r-g)/(MAX-MIN)+240).toFixed(3)
    return {H: parseFloat(H),S:parseFloat(S),L:parseFloat(L)}
}
```

### HLSL

```hlsl
// 输入参数名为 RGB
/**
拆分RGB的颜色通道值
*/
float r_value = RGB.r;
float g_value = RGB.b;
float b_value = RGB.b;
/**
计算出RGB各通道中的最大值和最小值
*/
float max_value = max(max(r_value, g_value), b_value);
float min_value = min(min(r_value, g_value), b_value);
float delta = max_value - min_value;
// 计算转换后的L通道值
float L = (max_value + min_value) / 2;
// 初始化返回结果向量
float3 HSL = (0, 0, L);
// L 通道等于0的特殊情况
if(L == 0 || delta == 0){
    HSL.x = 0;
    HSL.y = 0;
    return HSL;
}
// 计算返回结果的S通道值
if(L > 0 && L <= 0.5){
    HSL.y = (max_value - min_value) / (max_value + min_value);
} else {
    HSL.y = (max_value - min_value) / (2 - max_value - min_value);
}
// 计算返回结果的H通道值
if(max_value == r_value && g_value >=b_value ){
    HSL.x = (60 * (g_value - b_value) / (max_value - min_value));
}
if(max_value == r_value && g_value < b_value){
    HSL.x = (60 * (g_value - b_value) / (max_value - min_value) + 360);
}
if(max_value == g_value){
    HSL.x = (60 * (b_value - r_value) / (max_value - min_value) + 120);
}
if(max_value == b_value){
    HSL.x = (60 * (r_value - g_value) / (max_value - min_value) + 240);
}
return HSL;
```