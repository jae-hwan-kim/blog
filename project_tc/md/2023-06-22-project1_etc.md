---
title: "트센 etc"
categories:
    - 42project
tags:
    - 42seoul
    - 42 project
    - web socket
    - Rest API

last_modified_at: 2023-06-22T20:30:28
---

## 연결된 socket client 수 세기!

소켓에 연결된 client 수를 알고 싶었다... 2 ~ 3 일 정도 고통받았던 것 같다. 해결 방법은 `server` 객체 생성 시 옵션 설정에 있었다.

`nest JS` 는 `@WebSocketGateway` 데코레이터를 사용하는데, 옵션을 설정할 수 있다.

결론을 먼저 얘기하면,

* `namespace` 설정이 없다면, `server: Server` 로 객체를 생성하고 `this.server.engine.clientsCount` 로 

* `namespace` 설정이 있다면, `server: Namespace` 로 객체를 생성하고 `const clientsCount = this.server.sockets.size;` 로 

`client` 수를 알 수 있다. 아래 코드에 주석으로 표시된 `1`, `2`, `3` 을 참고하자!

부분 별로 위에는 namespace 설정이 없을 때, 아래가 없을 때이다.

```ts
@WebSocketGateway({
  // 1.
  // namespace 설정이 없음.
  namespace: 'game',
  ...
})
export class GameGateway
  implements OnGatewayInit, OnGatewayConnection, OnGatewayDisconnect
{
  ...
  @WebSocketServer()
  // 2.
  // server: Server;
  server: Namespace;

  afterInit() { ... }

  async handleConnection(client: Socket) {
    ...
    // 3.
    // const clientsCount = this.server.engine.clientsCount;
    const clientsCount = this.server.sockets.size;
    console.log(`Connected clients: ${clientsCount}`);
  }
  ...
}
```
