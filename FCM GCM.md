FCM과 GCM
===
출처 : <https://life-with-coding.tistory.com/28>

+ FCM,GCM
  + 서버에서 클라이언트 애플리케이션으로 메시지(알림)을 안정적으로 보낼수 있는 교차 플랫폼 메시징 솔루션
    + GCM
      + 구글에서 제공하는 서버에서 애플리케이션으로 푸시 메시지를 보낼 수 있는 서비스
      + android,ios 지원
      + 주소 : <https://android.googleapis.com/gcm/send>  
    + FCM
      + gcm의 상위 버젼
      + android, ios, mobild Web 지원
      + 주소 : <https://fcm.googleapis.com/fcm/send>
        + FCM 등록
          + 사용자는 FCM을 등록
          + FCM과 연결
          + FCM 등록 토큰을 리턴(to Client)
          + 클라이언트는 서버에 등록 토큰을 전달
        + 실제 사용 방법
          + <https://kwon8999.tistory.com/entry/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-FCM-%EA%B5%AC%ED%98%841%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%EC%85%8B%ED%8C%85-%EB%B0%8F-%EA%B5%AC%ED%98%84?category=881640>
          
          