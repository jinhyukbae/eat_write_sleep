# eat_write_sleep
플레이데이터 ai26기 파이널프로젝트 딥러닝 영어일기 서비스 
* 시연영상 : https://www.youtube.com/watch?v=bvmAax3yQds


## 다른 영어 일기 서비스와의 차이점
자연어 처리 모델 T5를 이용한 Grammar correction, Paraphrasing, Tag 기능 탑재

* Grammar correction : 사용자 틀린 문장을 입력했을 때 문법적으로 옳게 바꿔주는 기능 
* Paraphrasing : 사용자 입력 문장을 토대로 같은 뜻 다른 표현 문장 추천 해주는 기능
* Tag : 사용자 입력 문장을 summary 해서 자동으로 tag를 달아주는 기능


## 주제를 선택한 이유
* 데이터셋 가용 여부 : 해당 주제에 대한 데이터셋이 많은지 또 가공 되어 있는지 여부
  * jfleg 라는 영어 문법 교정 corpus가 존재하고 input(틀린 입력) output(교정된 값)으로 가공 되어있어 사용하기 쉬웠음   
* 서비스 구현 여부 : 서비스를 구현할 때 참고 자료 여부와 모델의 구현 가능 여부
  * huggingface, happytransformer 등 본 주제 서비스 구현에 필요한 정보를 획득할 수 있는 사이트가 많았음 
* 마켓 사이즈 여부 : 관련 분야에 대한 시장조사를 진행하여 사용자의 수요 여부, 경쟁자들을 조사
  *  
