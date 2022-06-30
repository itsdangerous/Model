## 0. Word2Vec 모델 선정 이유
* word2Vec, FastText, GloVe 세 가지 모델을 사용해 본 결과,
*  FastText는 OOA현상이 발생하지는 않았지만 그만큼 단어에 임베딩 된 벡터값이 낮아 비교적 낮은 성능을 보임.

*    GloVE는 co-occurrence를 판단하기 위해 최소 말뭉치 단어 개수의 2제곱 크기 만큼의행렬을 필요 -> 저차원 임베딩에선 Word2Vec이 성능면에서 유리하다고 판단.


## 1. data_processing.ipynb
*  wikipedia databse로 Raw Data 활용
* WikiExtractor를 이용하여 Raw Data 전처리
    * [Raw Data](https://dumps.wikimedia.org/kowiki/latest/kowiki-latest-pages-articles.xml.bz2)
    * [WikiExtractor](https://github.com/attardi/wikiextractor.git)

## 2. ko_wiki_nouns.txt
* proprocessing 된 데이터 -> 명사 추출
* [ko_wiki_nouns.txt](https://drive.google.com/file/d/13aZVnNJi6TqvpkD0ZPky9AFIV8P1-BS-/view?usp=sharing)

## 3. ko_w2v.ipynb
* 수집된 데이터로 Word2Vec 모델을 활용하여 임베딩 된 단어 벡터 추출
* 파라미터 설정 값
  * vector_size : 워드 벡터의 특징 값(임베딩 된 벡터의 차원) -> 100
  * window :중심 단어를 기준으로 주변 단어를 slicing할 word의 개수 -> 5
  * min_count : 단어 최소 빈도 수 제한(빈도가 적은 단어들은 학습에서 배제)
    * 보통 영어 문장에서는 비동사나 대명사와 같이 불필요한 단어가 한 문장당 5개 이하여서 5로 설정.
    * 한국어도 똑같이 적용.
    * 하지만 우리는 문장이 아니라 단어들만 추출하였고 min_count에 부합하지 못하면 배제시키므로 min_count의 차이만큼 정확도가 확실이 향상됨을 느낌.
  * workers = model 을 build할 때 사용할 Thread 개수 지정 -> 4
  * sg = 0 : CBOW
    * sg = 1 : Skip-gram
    * 우리는 단어를 입력받아 그 단어를 통해 주변 단어를 예측할 것이기 때문에 CBOW를 사용할 것.
  * 그 외 파라미터 값 : default

## 4. ko_w2v_model
* 학습된 모델
* [ko_w2v_model](https://drive.google.com/file/d/1P0XW4B3Agyzemg4T961zynWOQPmoDuU_/view?usp=sharing)
