[100만 달러짜리 빠른 앱을 만드는 비법 전수](https://tv.naver.com/v/15353556)
===
* 앱이 속도가 느려지는 이유
  * 복잡한 기능과 요구사항
  * 화려한 디자인
  * 애니메이션 기능
* 랜더링
  * 하나으 프레임을 그려내느 과정
* 안드로이드에서는 화면 갱신에 실패할경우 프레임 드랍이 발생한다. 
* 과정
  1. Button이 CPU에 의해 폴리고 텍스처로 변환
  2. 변환한 데이터는 OpenGL에 의해 CPU에서 GPU로 전달
  3. 레스터화르 거치 화면ㅇ 나타남
* **랜더링 성능의 핵심은 GPU의 메모리 적재되 데이터 관리**

>> View 성능 올리는 꿀팁
* 오버 드로잉 줄이기 (같은 픽셀에 여러번 덫 칠하는 것)
  * 예를들어서 부모뷰와 자식뷰의 동일한 백그라운드 색 사용
* 투명도 사용 줄이기
  * 부가적인 연산이 필요함
* 커스텀 뷰 사용시
  * onDraw() 에서 메모리 초기화 작업 삼가
  * onDraw(), onMeasure(), onLayout() 메서드가 자주 호출 되지 않도록 한다.
  * 무분별한 invalidate(), requestLayout() 삼가
* ConstraintLayout 사용하기
* ViewStub 사용
  * 초기화 지연
  * 사용자가 빠르게 스크룰 가능하도록 불필요한 레이아웃의 전개를 지연하고 전개시기를 늦추는 방법으로 성능 개선
* RecyclerView 퍼포먼스 향상
  * 부분적으로 아이템들을 갱신 (변경된 부분을 확실히 알고 있다면 이 메서드를 호출하는것이 더 빠름)
    * notifyItemChanged
    * notifyItemIserted
    * ..
    * .
  * DiffUtil
    * 변경된 부분만 갱신하도록 도와주는 유틸클래스
    * 반드시 구현해야 하는 DiffUtil.Callback 메서드
      * getOldListSize : 이전 리스트의 사이즈를 반환
      * getNewListSize : 새로운 리스트의 사이즈를 반환
      * areItemsTheSame : 두 아이템이 같은 아이템인지 검사한다.
      * areContentsTheSame : 두 아이템의 내용이 같은지 검사
  * setHasFixedSize 호출하기
    * RecyclerView의 크기가 어댑터의 내용에 의존하지 않는다는것을 알고있다면 어댑터의 아이템이 추가/제거 될때마다 RecyclerView의 크기가 변경되야하는지 알수있기 때문에 성능을 개선할수 있음
  * setItemViewCacheSize(Int) 호출하기
    * 아이템 View가 Pool로 들어가기 전에 유지되는 캐시의 사이즈를 결정
    * 아이템 View가 화면밖으로 사라졌다가 나타나도 onBindViewHolder Callback 메서드 호출없이 해당 View를 그대로 유지하기 떄문에 성능 개선
  * setRecycledViewPool(RecyclerViewPool) 호출하기
    * 플레이스토어 앱과 같은 앱처럼 중첩된 Recycler View를 사용할때 필요
    * 밖과 안의 ViewPool 공유
  * setHasStableIds(true) 호출하기
    * 아이템에 대해 고유 식별자를 부여하여 동일한 아이템에 대해 onBindViewHolder 호출을 방지하여 성능을 개선한다.
    * 이미 바인드된적이 있는 아이템에 대해서 재 바인드되지않도록 하는 방법
    
>> 앱 성능을 개선하기 위한 도구
* Layout Inspector
* 프로파일러
* Lint
  * 코드 스캔 도구
* GPU 랜더링 속도 프로파일링(개발자옵션에서 설정 가능)
* GPU 오버드로우 시각화(개발자옵션 -> 하드웨어 가속 랜더링 -> GPU 오버드로우 디버그)
  * 트로 컬러 : 오버드로 없음
  * 파란색 : 1회
  * 녹색 : 2회
  * 분홍 : 3회
  * 빨간색 : 4회
  * 반드시 파란색으로 나올필요는 없지만 유용함
    
