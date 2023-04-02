# Code-Injection

## Kết quả chạy baseline 
| Methods | Naïve Bayes | Decision Tree | Random Forest |  Logistic Regression | AdaBoost |
| :---: | :---: | :---: | :---: | :---: | :---: |
| BOW | 0.83 | 0.96 | 0.96 | 0.95 | 0.56 |
| TF-IDF | 0.87 | 0.96 | 0.96 | 0.95 | 0.56 |
| Word2Vec | 0.48 | 0.94 | 0.94 | 0.54 | 0.40 |

- Kết quả chạy baseline: Baseline.ipynb
- Hiện tại đang có một số vấn đề:
  + Data imbalance
  + Word2Vec có kết quả không tốt khi kết hợp với các bộ classifiers thuần (check lại code) và cần thử nghiệm thêm với một vài neural classifiers (CNN,...)

## Note về CAPEC data
- Data được phân tích và xử lý trong file: Data_Processing.ipynb
- Có 2 trường attack ko có tấn công (33 - HTTP Request Smuggling và 248 - Command Injection) trong bộ dataset multiclass. Lý do có thể vì hai trường attack này giao với các trường attack khác (multilabel)
- Tổng cộng các loại tấn công (đã bỏ 2 loại attack bên trên): 12 (bao gồm normal)
000 - Normal: 226509
272 - Protocol Manipulation: 6924
242 - Code Injection: 13792
88 - OS Command Injection: 3074
126 - Path Traversal: 17595
66 - SQL Injection: 248093
16 - Dictionary-based Password Attack: 836 X
310 - Scanning for Vulnerable Software: 2382
153 - Input Data Manipulation: 1387
274 - HTTP Verb Tampering: 4047 X
194 - Fake the Source of Data: 55982
34 - HTTP Response Splitting: 19134
- Mỗi sample có rất nhiều trường dữ liệu, tuy nhiên chỉ có 1 số attribute giúp classify web attacking
- Thử nghiệm với concat 3 trường dữ liệu: request_method, request_http_request và request_body (với method POST)
- Thử nghiệm với một vài kiểu tấn công, và để lại một vài kiểu tấn công có cùng variance với bộ dataset để nghiên cứu Transfer Learning
- Các kiểu tấn công sử dụng trong dataset: 272 - Protocol Manipulation, 242 - Code Injection, 126 - Path Traversal, 66 - SQL Injection, 310 - Scanning for Vulnerable Software, 153 - Input Data Manipulation, 194 - Fake the Source of Data, 34 - HTTP Response Splitting
Kiểu tấn công dành cho Transfer Learning: OS Command Injection
- Hiện tại đang chưa tích hợp bộ dataset CSIC 2010-2012 (Bao gồm XSS attack và SQLi attack)

