# Chapter 03 제출 답안 양식. 데이터의 첫인상 읽기

> 주 제출물은 실행 완료 Notebook `chapter03/chapter03.ipynb`입니다. 이 양식의 항목을 Notebook의 Markdown 셀로 추가해 작성합니다.

## 0. 제출 정보
- 이름: 김지인
- GitHub ID: jiin-0
- 작성일: 2026.09.23
- 최종 제출 URL: https://github.com/jiin-0/llm-data-analysis-study/blob/b0da74a653a32ca4fbd907e9a3e2600874819d4a/chapter03/ch03_data_overview.ipynb

## 1. 데이터 로딩과 구조 확인
### 실행/결과
- 4개 CSV 로딩 여부: 로딩 성공(CSV to Dataframe)
- 각 데이터 shape: |customers(150,6)|products(100,4)|orders(300,5)|order_items(764,5)|
- 주요 컬럼:|customers.customer_id|products.product_id|orders.order_id|orders.customer_id|order_itmes.order_order_item_id|order_items.order_id|order_items.product_id
- dtypes에서 주목한 컬럼: signup_date, order_date - 모두 날짜형데이터이나 str(문자형데이터)로 나타났다.

### Evidence
![데이터 구조 확인](images/step01_structure.png)

### 결과 관찰
4개의 CSV 파일이 모두 데이터프레임형식으로 로딩 되었다. 각 파일이 몇개의 행과 열로 구성되어있는지 shape을 통해 확인하였고, 행이 가장 많은 파일은 order_items로 나타났다. head(), tail()을 통해 상위 5열, 하위 5열의 데이터를 확인하여 각 컬럼에 데이터가 어떤 형식으로 들어있는지 직관적으로 확인하였다. info(), columns를 이용하여 각 파일의 컬럼 정보를 확인하였으며, 파일간 공통적인 컬럼(customer_id, product_id, order_id)이 관찰되었다. 또한, 직관적으로 날짜형인 데이터(signup_date, order_date)가 실제 dtypes로 확인할 결과 문자형으로 확인되었다.

### 나의 해석과 판단
order_items의 행이 orders보다 많으므로 주문 1건에 여러개의 아이템을 구매한 경우가 포함되어 있다고 해석할 수 있다. 또한, customers의 customer_id를 통해 고객을, orders의 order_id를 통해 주문을, products의 products_id를 통해 상품을 구분할 수 있을 것이다. 또한 파일간 공통적인 컬럼들을 통해 파일을 연결할 수 있을 것이다.
현재 dtypes로 확인한 결과 signup_date와 order_date의 형식이 문자열이므로 날짜로 인식되고 있지 않다. 따라서 이를 목적에 따라 날짜형으로 변환하는 과정이 필요하다. 또한, orders.order_id, customers.customer_id가 파일 내에서 중복되지 않는지 확인이 필요하다. 

### 업무·분석적 의미
구조를 먼저 확인하지 않을 경우 각 파일에 어떤 컬럼들, 어떤 정보들이 있는지 파악이 되지 않는다. 또한 각 파일 사이 연결되는 컬럼이 있는지 확인하지 않으면 파일간 연결 시 시작을 할 수 없다.
각 컬럼의 형식을 확인하여 기대되는 형식과 실제 형식이 일치하는지 확인하여 데이터가 원하는 형식으로 읽혔는지, 데이터에 오류가 있는지 간단히 확인할 수 있다. 이를 통해 추후 이어질 분석에서 발생할 형식에 따른 오류 발생을 줄일 수 있다.
또한 파일간 공통적인 컬럼이 customer_id, product_id, order_id의 형식이 현재 모든 파일에서 일치하므로 이를 기준으로 파일을 연결할 때 오류가 여지를 줄일 수 있다.

### 한계와 추가 확인 사항
각 파일에 컬럼이 무엇이 있고, 데이터 형식이 무엇인지, 상하위 5개의 데이터를 확인하였다. 그러나 실제 모든 데이터에 오류가 있는지 확인하지 못했다. 따라서 가장 큰 틀에서 데이터를 파악했기 때문에 세부적인 데이터를 확인하는 과정이 필요하다.

## 2. 결측·중복·키 품질
- 주요 ID 결측: X
- 주요 ID 중복: X
- 전체 행 중복: X

![결측 중복 점검](images/step02_quality.png)

### 결과 관찰
결측 관찰 결과, 모든 column에서 결측이 관찰되지 않았다. 주요 ID 중복 관찰결과, customers.customer_id, products.product_id, orders.order_id에서 중복이 관찰되지 않았다. order_items.order_id에서는 중복이 관찰되었다. duplicated()로 관찰한 결과 전체 행 중복 또한 관찰되지 않았다.

### 나의 해석과 판단
어떤 문제를 먼저 처리해야 하는지 우선순위를 작성하세요.
데이터 관찰 결과 주요 컬럼에서 결측과 중복이 나타나지 않았다. order_itmes.order_id에서는 중복이 관찰되었으나 order_items.order_id은 중복가능(한 주문에 여러 상품이 있을 수 있음.)

### 업무·분석적 의미



### 한계와 추가 확인 사항

## 3. 숫자형·범주형·날짜 점검
- 숫자형 범위에서 주목한 값:
- 범주형 빈도에서 주목한 값:
- 날짜 변환 실패 건수:
- 날짜 범위:

![기본 분포와 날짜 확인](images/step03_distribution.png)

### 결과 관찰

### 나의 해석과 판단
이상해 보이는 값이 실제 오류인지 업무적으로 가능한 값인지 구분하기 위해 무엇을 더 확인해야 하는지 작성하세요.

### 업무·분석적 의미

### 한계와 추가 확인 사항

## 4. CSV 간 키 관계 검증
- 없는 `customer_id`:
- 없는 `order_id`:
- 없는 `product_id`:

![PK FK 관계 검증](images/step04_relationship.png)

### 결과 관찰

### 나의 해석과 판단
키 관계 문제가 발견되었다면 바로 삭제하면 안 되는 이유를 작성하세요.

### 업무·분석적 의미

### 한계와 추가 확인 사항

## 5. LLM 구조 설명 검증
- LLM에 제공한 Safe Context:
- LLM이 제안한 추가 점검:
- 실제 데이터에서 확인한 항목:
- 채택/수정/보류한 내용:

![LLM 구조 검토](images/step05_llm.png)

### 나의 해석과 판단
LLM 제안 중 가장 유용했던 것과 가장 조심해야 할 것을 작성하세요.

### 한계와 추가 확인 사항

## 6. Chapter 03 최종 판단
### 데이터의 첫인상 3가지
1.
2.
3.

### 다음 Chapter 전에 반드시 확인/처리해야 할 항목
1.
2.
3.

### 현재 데이터만으로 단정할 수 없는 것

## 최종 제출 체크
- [ ] Notebook을 처음부터 끝까지 실행했습니다.
- [ ] 오류 셀이 남아 있지 않습니다.
- [ ] 핵심 Evidence를 첨부했습니다.
- [ ] 관찰과 해석을 구분했습니다.
- [ ] 개인정보/Secret이 없습니다.
- [ ] `chapter03/chapter03.ipynb`가 GitHub에서 정상 표시됩니다.
- [ ] 최종 Notebook 파일 URL을 제출합니다.
