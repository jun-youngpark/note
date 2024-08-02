# BigQuery에서 데이터 삽입(INSERT) 방법

Google BigQuery에서는 여러 가지 방법으로 데이터를 삽입할 수 있습니다. 이 문서에서는 SQL을 통한 데이터 삽입, 데이터 업로드, 스트리밍 삽입, 그리고 Data Transfer Service를 이용한 방법을 설명합니다.

## 1. SQL을 통한 데이터 삽입

BigQuery에서는 SQL을 사용하여 데이터를 삽입할 수 있습니다. `INSERT` 문을 사용하여 테이블에 새 행을 추가할 수 있습니다.

```sql
INSERT INTO dataset_name.table_name (column1, column2, column3)
VALUES ('value1', 'value2', 'value3');
```

2. Data Ingestion (데이터 업로드)
CSV, JSON 파일 업로드
CSV, JSON 형식의 파일을 Google Cloud Storage에 업로드한 후 BigQuery 테이블로 로드할 수 있습니다.

Google Cloud Storage
데이터를 Google Cloud Storage에 저장한 후 BigQuery 테이블로 로드할 수 있습니다.

Google Sheets
Google Sheets에서 직접 BigQuery로 데이터를 가져올 수 있습니다.

3. Streaming Inserts (스트리밍 삽입)
BigQuery의 스트리밍 삽입 기능을 사용하여 실시간으로 데이터를 삽입할 수 있습니다. 이는 실시간 데이터 분석이 필요한 경우에 유용합니다.

python 
```
from google.cloud import bigquery

client = bigquery.Client()

table_id = 'your-project.your_dataset.your_table'

rows_to_insert = [
    {u"column1": u"value1", u"column2": u"value2"},
    {u"column1": u"value3", u"column2": u"value4"},
]

errors = client.insert_rows_json(table_id, rows_to_insert)
if errors == []:
    print("New rows have been added.")
else:
    print("Encountered errors while inserting rows: {}".format(errors))
```
4. Data Transfer Service (데이터 전송 서비스)
Scheduled Queries (예약 쿼리)
정기적으로 실행되는 쿼리를 통해 데이터를 삽입하거나 업데이트할 수 있습니다.

Data Transfer Service
외부 데이터 소스에서 BigQuery로 데이터를 자동으로 로드할 수 있습니다.
