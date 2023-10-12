# KoBERT

## 📌 kobert 를 활용한 댓글 감정 분석 댓글의 TfidfVectorizer 를 통하여 해시태그 추출 
![image](https://github.com/harim061/KoBERT/assets/90364684/58d13114-1e3e-438f-bb96-f5e1b0d864ff)

![image](https://github.com/harim061/KoBERT/assets/90364684/1e5ffa4d-6733-4bdb-94cc-f33c48ffc468)

## 📌 Point

- koBERT 모델을 활용하여 텍스트 데이터의 감정을 분석
- keybert 모델을 활용하여 유튜브 제목과 비슷한 댓글의 키워드 추출

## 📌 Code [감정 분석]

1. 데이터 전처리
    - 주어진 데이터셋에서 '발화문'과 '상황' 열을 추출하고, '상황' 열의 감정 레이블을 숫자로 변환
    - 데이터를 문장과 해당 문장의 레이블로 이루어진 리스트로 변환
2. BERT 모델 로딩
    - `Hugging Face`의 `transformers 라이브러리`를 사용하여 사전 훈련된 BERT 모델과 토크나이저를 로드
    - 한국어 BERT 모델인 'skt/kobert-base-v1'을 사용
3. 학습 설정
    - 손실 함수로 `CrossEntropyLoss`를 사용. 다중 클래스 분류 문제에 적합한 손실 함수
    - 옵티마이저로 `AdamW`를 사용

## 📌 Code [키워드 추출]

1. KeyBERT를 사용한 키워드 추출
    - KeyBERT 모델을 초기화하고, **`extract_keywords`** 메서드를 사용하여 CSV 텍스트 데이터의 키워드를 추출
    - `여기서는 MMR (Maximum Marginal Relevance)` 방식을 사용하여 다양성을 높이는 키워드를 추출
2. 문장 임베딩 및 유사도 계산
    - SentenceTransformer를 사용하여 문장 임베딩을 생성
    - 주어진 쿼리 문장의 임베딩과 CSV 텍스트 데이터 내의 각 문장의 임베딩 사이의 코사인 유사도를 계산
    - 유사도가 가장 높은 상위 5개의 문장을 출력
3. TF-IDF를 사용한 키워드 추출
    - 불용어를 제외하고 TF-IDF 벡터라이저를 사용하여 CSV 텍스트 데이터의 키워드를 추출
    - 전체 문서에 대한 각 키워드의 중요도를 계산하고, 중요도가 높은 상위 15개의 키워드를 출력
