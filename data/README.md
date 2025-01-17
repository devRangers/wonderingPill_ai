## 데이터셋 구축

#### 의약품안전나라 의약품 낱알식별 데이터셋

- [pills_data.origin.csv](https://nedrug.mfds.go.kr/pbp/CCBGA01/getItem?totalPages=4&limit=10&page=2&&openDataInfoSeq=11)

**1. 의약품 낱알식품.csv의 url로부터 알약 이미지 다운로드**

```python
$ cd data
$ python download_url_to_img.py
```

**2. 다운로드한 원본 이미지 배경 전처리**

```python
$ python grabcut.py
```

**3. 이미지 전경 전처리 custom 기능 동작을 원할 경우**

- custom할 알약 품목명 리스트를 입력 후 실행
- 마우스 왼쪽 버튼 드래그: 전경 복구
- 마우스 오른쪽 버튼 드래그: 전경 제거
- Enter: 전처리 후 이미지 보기 및 저장
- q : quit

```python
$ python grabcut_custom.py
```

**4. 전처리 된 이미지 augmentation**

```python
$ python img_augmentation.py
```

**5. 최종 알약 데이터 셋 & label 파일 생성**

- pills_data.available_in_api.preprocess.csv 생성

```python
$ python make_pill_df.py
```

---

#### 제형 분류 학습용 데이터셋 ####
1. pills_data.available_in_api.shape.csv
- api로 알약 정보를 받아올 수 있는 알약 이미지 데이터
- 총 9가지의 제형 라벨 존재
- 라벨 별 데이터 불균형 문제

2. pills_data.shape.balanced.csv
- 제형 분류에 굳이 api로 알약 정보를 받아올 수 있는 알약 이미지 데이터만 사용할 필요는 없음
- 정보를 받아올 수 없어 사용하지 않았던 알약 이미지 데이터로부터 부족한 제형 알약 이미지를 보충 
---

## data 폴더 구성

```
📦data
┣ 📂img
┃ ┣ 📂200808876
┃ ┃ ┣ 📜200808876.jpg
┃ ┃ ┣ 📜200808876_0.jpg
┃ ┃ ┣ ...
┃ ┃ ┗ 📜200808876_100.jpg
┣ 📂label
┃ ┗ 📜pill_label.pkl
┣ 📜download_url_to_img.py
┣ 📜grabcut.py
┣ 📜grabcut_custom.py
┣ 📜img_augmentation.py
┣ 📜make_pill_df.py
┣ 📜pills_data.available_in_api.csv
┣ 📜pills_data.available_in_api.preprocess.csv
┣ 📜pills_data.csv
┣ 📜pills_data.preprocess.csv
┗ 📜README.md
```
