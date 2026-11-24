### 1. Câu lệnh SELECT
- Cú pháp:
  ```
  Truy vấn một cột cụ thể: SELECT column, another_column, … FROM mytable;
  Truy vấn tất cả các cột: SELECT * FROM mytable;
  ```
### 2. Truy vấn có ràng buộc
- Câu truy vấn Select có ràng buộc:
  ```
  SELECT column, another_column, … FROM mytable
  WHERE condition
      AND/OR another_condition
      AND/OR …;
  ```
- | Toán tử      |Điều kiện| Ví dụ |
  | -------      | --------- | ----- |
  |=,!=,<,<=,>,>=|Toán tử so sánh |col_name != 4|
  |BETWEEN … AND...|Số nằm trong phạm vi của hai giá trị (đã bao gồm)|col_name BETWEEN 1.5 AND 10.5|
  |NOT BETWEEN … AND …|Số không nằm trong phạm vi của hai giá trị (đã bao gồm)|col_name NOT BETWEEN 1 AND 10|
  |IN (…)|Số tồn tại trong danh sách|	col_name IN (2, 4, 6)|
  |NOT IN (…)|Số không tồn tại trong danh sách|col_name NOT IN (1, 3, 5)|
- | Toán tử | Điều kiện | Ví dụ |
  |:---:|---|---|
  | `=` | So sánh chuỗi chính xác, phân biệt chữ hoa và chữ thường (**chú ý chỉ có một dấu bằng**) | `col_name = "abc"` |
  | `!=` hoặc `<>` | So sánh chuỗi không bằng chính xác, phân biệt chữ hoa và chữ thường | `col_name != "abcd"` |
  | `LIKE` | So sánh chuỗi chính xác, không phân biệt chữ hoa và chữ thường | `col_name LIKE "ABC"` |
  | `NOT LIKE` | So sánh chuỗi không bằng, không phân biệt chữ hoa và chữ thường | `col_name NOT LIKE "ABCD"` |
  | `%` | Được sử dụng ở bất kỳ vị trí nào trong chuỗi để khớp với một chuỗi gồm 0 hoặc nhiều ký tự (chỉ sử dụng với `LIKE` hoặc `NOT LIKE`) | `col_name LIKE "%AT%"` (khớp với `"AT"`, `"ATTIC"`, `"CAT"` hoặc thậm chí `"BATS"`) |
  | `_` | Được sử dụng ở bất kỳ vị trí nào trong chuỗi để khớp với một ký tự đơn (chỉ sử dụng với `LIKE` hoặc `NOT LIKE`) | `col_name LIKE "AN_"` (khớp với `"AND"`, nhưng không khớp với `"AN"`) |
  | `IN (...)` | Chuỗi tồn tại trong một danh sách | `col_name IN ("A", "B", "C")` |
  | `NOT IN (...)` | Chuỗi không tồn tại trong một danh sách | `col_name NOT IN ("D", "E", "F")` |
### 3. Lọc và sắp xếp kết quả truy vấn
- Truy vấn có kết quả duy nhất
  ```
  SELECT DISTINCT column, another_column, …
  FROM mytable
  WHERE condition(s);
  ```
- Vì từ khóa `DISTINCT` sẽ loại bỏ một cách mù quáng các hàng trùng lặp, nên chúng ta sẽ tìm hiểu cách loại bỏ các hàng trùng lặp dựa trên các cột cụ thể bằng cách sử dụng nhóm và mệnh đề `GROUP BY`.
- Truy vấn với kết quả được sắp xếp
  ```
  SELECT column, another_column, …
  FROM mytable
  WHERE condition(s)
  ORDER BY column ASC/DESC;
  ```
- Truy vấn có hàng giới hạn
  ```
  SELECT column, another_column, …
  FROM mytable
  WHERE condition(s)
  ORDER BY column ASC/DESC
  LIMIT num_limit OFFSET num_offset;
  ```
- Trong đó:
  - `Limit` là giới hạn số người được chọn
  - `OFFSET` là số bị loại bỏ
- Ví dụ: Lấy sinh viên có điểm cao thứ 4 và thứ 5 của lớp 'CNTT1' (bỏ qua 3 người đầu tiên):
  ```
  SELECT TEN, DIEM
  FROM SINHVIEN
  WHERE LOP = 'CNTT1'
  ORDER BY DIEM DESC
  LIMIT 2 OFFSET 3;
  ```
### 4. Truy vấn nhiều bảng với JOINS
- Chọn truy vấn bằng INNER JOIN trên nhiều bảng
  ```
  SELECT column, another_table_column, …
  FROM mytable
  INNER JOIN another_table 
      ON mytable.id = another_table.id
  WHERE condition(s)
  ORDER BY column, … ASC/DESC
  LIMIT num_limit OFFSET num_offset;
  ```
### 5. UNION
- Cú pháp:
  ```
  SELECT column1, column2
  FROM table1
  UNION
  SELECT column1, column2
  FROM table2;
  ```
- Ví dụ sử dụng: Lấy danh sách quốc gia duy nhất từ hai bảng Customers và Suppliers:
  ```
  SELECT Country FROM Customers
  UNION
  SELECT Country FROM Suppliers;
  ```
### 6.SUBSTRING
- Cú pháp:
  ```
  SUBSTRING(string, start, length)
  Hoặc
  SUBSTRING(string FROM start FOR length)
  ```
- Ví dụ:
  ```
  -- Lấy 6 ký tự đầu từ vị trí 1 -> kết quả: 'PAVIET'
  SELECT SUBSTRING('PAVIETNAM', 1, 6);
  ```
