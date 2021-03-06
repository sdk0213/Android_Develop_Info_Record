안드로이드 생명주기
===

홈버튼을 누르고 와서 다시 동영상을 재생 시키기위해서는 복귀할때의 설정을 다시 해줘야 하는데 이를 하기위해서는
안드로이드 생명주기를 파악할 필요가있음

Activity - 수명 주기
1. onCreate()
2. onStart()
3. onResume()
4. onPause()
5. onStop()
6. onDestroy()

<img src="https://developer.android.com/guide/components/images/activity_lifecycle.png?hl=ko" width="450px" height="450px" title="px(픽셀) 크기 설정" alt="RubberDuck"></img><br/>

**몇 가지 예외를 제외하고 앱은 백그라운드에서 실행될 때 Activity를 실행할수 없다.

onCreate()
---
* savedInstanceState : Activity 이전 저장 상태가 포함된 Bundle 객체, 전에 저장된것 불러오는것
* 시스템이 먼저 Activity를 생성할 때 실행되는 것으로, 필수적으로 구현해야 한다.
* onCreate() 메서드가 실행을 완료하면 시작됨 상태가 되고, 시스템이 연달아 onStart()와 onResume() 메서드를 호출한다.

onStart()
---
* onStart()가 호출되면 Activity가 사용자에게 보이게 되고, 앱은 Activity 포그라운드에 보내 상호작용할 수 있도록 준비함

onResume()
---
* 앱이 사용자와 상호작용하는 단계
* 전화가 오거나, 다른 Activity로 이동하거나, 기기화면이 꺼지고 다시 복귀할때
* ON_START 이벤트 이후에 무언가를 초기화하는 경우, ON_STOP 이벤트 이후에 이를 해제하거나 종료
* ON_RESUME 이벤트 이후에 초기화하는 경우, ON_PAUSE 이벤트 이후에 해제
* LifecycleObserver 사용

onPause()
---
* onPause()를 사용하여 애플리케이션 또는 사용자 데이터를 저장하거나, 네트워크 호출을 하거나, 데이터베이스 트랜잭션을 실행해서는 안된다.
* 

onStop()
---
* Activity가 사용자에게 더 이상 표시되지 않으면 중단됨 상태에 들어가고 시스템은 onStop() 콜백을 호출
* Activity가 중단됨 상태에 들어가면 메모리안에 머무르게 되기때문에 사용자가 EditText위젯에 텍스트를 입력하면 해당 내용이 저장되어서 이를 저장하고 복원할필요없음
* 시스템이 다시 시작되면 onRestart(), 종료되면 onDestory()를 호출한다.

onDestory()
---
* Activity가 소멸되기 전에 호출된다.
* 1. finish()가 호출되거나 사용자가 Activity를 닫을때
* 2. 기기회전 또는 멀티 윈도우 모드에서 시스템이 일시적으로 Activity를 소멸시키는 경우
* 소멸되는 이유를 결정하는 로직을 입력하는 대신 ViewModel 객체를 사용하여 Activity의 관련 뷰 데이터를 포함해야 한다.


정보 제공자 :
[programmingfbf7290.tistory](https://programmingfbf7290.tistory.com/entry/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%95%A1%ED%8B%B0%EB%B9%84%ED%8B%B0Activity-%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0-%EC%B4%9D%EC%A0%95%EB%A6%AC)



활용
---
* onCreate : 초기화 처리, 뷰 생성 등
* onStart : 통신이나 센서 처리 시작
* onRestart : 보통 아무 작업 안 함.
* onResume : 필요한 애니메이션 실행 등의 화면 갱신 처리
* onPause : 애니메이션 등 화면 갱신 처리 정지 또는 일시 정지할 때 필요 없는 리소스 해체하거나 필요한 데이터 영속화
* onStop : 통신이나 센서 처리 정지
* onDestroy : 필요 없는 리소스 해제, 액티비티 참조 정리


호출 순서
---
1. 시작할 때 : onCreate -> onStart -> onResume
2. 화면 회전할 때 : onPause -> onStop -> onDestroy -> onCreate -> onStart -> onResume
3. 다른 액티비티가 위에 뜰 때/전원 키로 화면 OFF할 때/홈 키 : onPause -> onStop
4. 백 키로 액티비티 종료 : onPause -> onStop -> onDestory
5. 백 키로 기존 액티비티에 돌아올 때/홈 키로 나갔다가 돌아올 때 : onRestart -> onStart -> onResume
6. 다이얼로그 액티비티나 투명 액티비티가 위에 뜰 때 : onPause



