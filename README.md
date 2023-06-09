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
  * 한국인의 영어 교육열.. “한 달 200만원 영어 유치원”, 코로나시대, 사교육 1위 과목 '영어' 같은 통계에 의거하여 수요가 충분함을 확인했고 영어일기만 쓰는 사이트 or 문법교정만 해주는 사이트,이음동의어 찾아주는 사이트는 많았으나 이 서비스들이 다 합쳐진 것은 없었음 


## 어려웠던점

### 모델링
* 본 데이터셋의 크기가 너무 방대해서 (1TB 이상) 훈련하는 데 문제가 있었음
* 열악한 컴퓨터 환경 (내장그래픽 노트북, 1050TI GPU 사양의 데스크탑) 때문에 훈련하는 데 문제가 있었음
* COLAB PRO 환경에서도 컴퓨팅 자원 금방 써버리고 런타임 유지가 1일 이상 안돼서 훈련하는 데 문제가 있었음

### 해결하기 위한 노력
데이터셋을 잘라서 훈련 시키는 시도
huggingface 에서 pretrained 된 모델 사용 시도 

### 문법 교정 모델의 동어 반복의 오류
* 짦은,의미 없는 문장을 입력하면 동어 반복되는 오류 
  * im happy -> im happy im happy 
  * adqwfqwfqwe -> adqwfqwfqweadqwfqwfqwe
* 디코딩 파라미터 튜닝(Greedy Search, Beam Search, Sampling, Top-k Sampling ...) 등을 시도하였으나 자연어 처리 모델 특유의 동어 반복의 문제는 해소 돼지 않았음
  * https://arxiv.org/abs/2002.02492 동어 반복 문제에 대한 논문    

### 디코더 파라미터 튜닝 전략
* Greedy Search
  * 타임스텝 t에서 가장 높은 확률을 가지는 토큰을 다음 토큰으로 선택하는 전략
* Beam Search
  * 각 타임스텝에서 가장 가능성 있는 num_beams개의 시퀀스를 유지하고, 최종적으로 가장 확률이 높은 가설을 선택하는 방법
* Sampling
  * 모델이 생각하는 다음에 올 토큰에 대한 확률분포에 따라 단어를 샘플링하는 방식으로 디코딩하는 전략
* Top-k Sampling
  * 가장 확률이 높은 K개의 '다음 단어들'을 필터링하고, 확률 질량을 해당 K개의 '다음 단어들'에 대해 재분배하는 전략
* Top-p (nucleus) sampling
  * 가능도 있는 k개의 단어로부터 샘플링하는 대신, 누적 확률이 확률 p에 다다르는 최소한의 단어 집합으로부터 샘플링

* reference : https://huggingface.co/blog/how-to-generate?fbclid=IwAR19kbEiW_sF19TeSr4BE4jQZSIqz0GzOFD2013fIGEH32DReW9pAFq6vDM



### 서비스 배포
* 부족한 자금 사정으로 free tier 인스턴스를 사용하다 보니 용량 부족 사태 발생 
 * 필요 라이브러리,모델 들의 용량이 너무커서 killed 되는 문제가 발생 (메모리, 용량 부족)

### 해결하기 위한 노력

임시파일 삭제, 로컬 캐시를 사용하지 않고 라이브러리 설치,스왑파일 생성 하는 등 여러가지 시도를 하였으나 서비스 배포 실패 


