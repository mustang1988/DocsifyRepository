# WebRTC源码分析

---

本源码分析的WebRTC源码版本为: 4147(m84)

[Chromium分支与版本号](https://chromiumdash.appspot.com/branches)

---

## 一次完整的WebRTC推拉流交互流程

```plantuml
@startuml 一次完整的WebRTC推拉流交互流程
entity 推流端
entity 信令服务
entity ICE服务
entity 收流端

activate 推流端

推流端 -> 信令服务: 1. 推流端与信令服务建立WebSocket连接

activate 信令服务

收流端 -> 信令服务: 2. 收流端与信令服务建立WebSocket连接

activate 收流端

信令服务 -> 推流端: 3. 信令服务通知推流端, 收流端已上线

推流端 -> 推流端: 4. 创建RTCPeerconnection对象
note left
const CallerPeerConnection = new RTCPeerConnection();
end note

推流端 -> 推流端: 5. 推流端获取本地摄像头和麦克风源
note left
const LocalStreams = await navigator
                        .mediaDevices
                        .getUserMedia({ video:true, audio:true });
end note

推流端  -> 推流端: 6. 推流端将获取到的本地摄像头及麦克风源加入到RTCPeerconnection对象中
note left
CallerPeerConnection.addStream(LocalStreams);
end note

推流端 -> 推流端: 7. 推流端创建Offer
note left
const OfferOptions = {
    offerToReceiveAudio: true,
    offerToReceiveVideo: true,
    voiceActivityDetection: true
};
const CallerOfferSDP = await CallerPeerConnection
                        .createOffer(OfferOptions);
end note

推流端 -> 推流端: 8. 推流端将Offer设置到本地描述信息中
note left
CallerPeerConnection.setLocalDescription(CallerOfferSDP);
end note

推流端 -> 信令服务: 9. 推流端将Offer发送到信令服务

信令服务 -> 收流端: 10. 信令服务将推流端发送来的Offer推送给收流端

收流端 -> 收流端: 11. 收流端创建RTCPeerconnection对象
note right
const ReceiverRTCPeerConnection = new RTCPeerConnection();
end note

收流端 -> 收流端: 12. 收流端将信令推送来的Offer设置到远端描述信息中
note right
ReceiverRTCPeerConnection.setRemoteDescription(Offer);
end note

收流端 -> 收流端: 13. 收流端创建Anwser
note right
const AnwserOptions = {
    offerToReceiveAudio: true,
    offerToReceiveVideo: true,
    voiceActivityDetection: true
};
const Anwser = ReceiverRTCPeerConnection.createAnwser(AnwserOptions);
end note

收流端 -> 收流端: 14. 收流端将创建的Anwser设置到本地描述信息中
note right
ReceiverRTCPeerConnection.setLocalDescription(Anwser);
end note

收流端 -> 信令服务: 15. 收流端将创建的Anwser发送到信令服务

信令服务 -> 推流端: 16. 信令服务将收流端发送来的Anwser推送给推流端

推流端 -> 推流端: 17. 推流端将信令服务推送来的Anwser设置到远端描述信息中
note left
CallerPeerConnection.setRemoteDescription(Anwser);
end note

推流端 -> ICE服务: 18. 推流端请求ICE服务获取自己的Relay NAT信息

activate ICE服务
ICE服务 -> 推流端: 19. ICE服务返回推流端的Relay NAT信息CallerCadicate

推流端 -> 信令服务: 20. 推流端将自己的CallerCadicate发送到信令服务

信令服务 -> 收流端: 21. 信令服务将推流端发送来的CallerCadicate推送给收流端

收流端 -> 收流端: 22. 收流端将收到的CallerCadicate设置到RTCPeerconnection对象中
note right
ReceiverRTCPeerConnection.addIceCandidate(CallerCadicate);
end note

收流端 -> ICE服务: 23. 收流端请求ICE服务获取自己的Relay NAT信息

ICE服务 -> 收流端: 24. ICE服务返回收流端的Relay NAT信息ReceiverCadicate

收流端 -> 信令服务: 25. 收流端将自己的ReceiverCadicate发送到信令服务

信令服务 -> 推流端: 26. 信令服务将收流端发送来的ReceiverCadicate推送给推流端

推流端 -> 推流端: 27. 推流端将信令推送来的ReceiverCadicate设置到RTCPeerconnection对象中
note left
CallerPeerConnection.addIceCandidate(ReceiverCadicate);
end note

推流端 <-> 收流端: 28. 推流端和收流端使用各自在RTCPeerconnection对象中持有的对方的Relay NAT信息建立端对端连接

推流端 <-> 收流端: 29. 推拉音视频流

@enduml
```

?> 源码分析基于上述一次完整流程中类出现JavaScript类的顺序进行, 会对该JS类对应的到WebRTC源码中的C++类进行逐一分析

|JavaScript类|涉及到的C++类|
|:-|:-|
|RTCPeerConnection|[PeerConnectionInterface](/repository/Libraries/WebRTC/docs/源码分析/PeerConnectionInterface.md#peerconnectioninterface-源码分析)|
|MediaStream|[MediaStreamInterface](/repository/Libraries/WebRTC/docs/源码分析/MediaStreamInterface.md#MediaStreamInterface-源码分析)|
|RTCSessionDescription|[SessionDescriptionInterface](/repository/Libraries/WebRTC/docs/源码分析/SessionDescriptionInterface.md#SessionDescriptionInterface-源码分析)<br/>[SetSessionDescriptionObserver](/repository/Libraries/WebRTC/docs/源码分析/SetSessionDescriptionObserver.md#SetSessionDescriptionObserver-源码分析)|
|RTCIceCandidate|[IceCandidateInterface](/repository/Libraries/WebRTC/docs/源码分析/IceCandidateInterface.md#IceCandidateInterface-源码分析)|

