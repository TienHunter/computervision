
## **Morphological Transformations**
### **dilation (phép dãn nở)**
Hàm `cv2.dilate` trong OpenCV được sử dụng để áp dụng phép toán dilation (nở) lên một ảnh nhị phân hoặc mặt nạ (mask). Phép nở giúp làm mở rộng các vùng sáng trong ảnh, làm cho các đối tượng sáng (trắng) trở nên lớn hơn. Điều này có thể hữu ích trong việc làm mượt các biên của đối tượng hoặc nối các vùng rời rạc lại với nhau.

```python
dilated = cv2.dilate(mask, kernel)
```
#### **Giải thích tham số**
- `mask`: Ảnh đầu vào, thường là ảnh nhị phân (được tạo ra từ phép thresholding hoặc các thao tác lọc).
- `kernel`: Ma trận kernel (hoặc structuring element) dùng để nở. Kernel này xác định kích thước và hình dạng của sự nở. Kernel này có thể là một ma trận vuông hoặc hình chữ nhật tùy thuộc vào mục đích của bạn.

#### **Cách hoạt động**
Phép toán **dilation** sẽ áp dụng kernel lên từng pixel của ảnh:
- Với mỗi pixel trong ảnh, nếu có bất kỳ pixel nào trong vùng của kernel có giá trị 255 (trắng), pixel trung tâm sẽ được thay đổi thành 255 (trắng).
- Với mỗi pixel trong ảnh, nếu có bất kỳ pixel nào trong vùng của kernel có giá trị 255 (trắng), pixel trung tâm sẽ được thay đổi thành 255 (trắng).

#### **Ứng dụng**
1. **Làm mịn biên của đối tượng**: Dilation giúp làm mềm và mở rộng biên của đối tượng.
2. **Kết nối các đối tượng rời rạc**: Nếu có các vùng sáng nhỏ bị phân tách, dilation có thể nối chúng lại với nhau.
3. **Tăng kích thước của đối tượng**: Dùng để mở rộng các đối tượng sáng trong ảnh.

### **erosion (mài mòn)**
Hàm `cv2.erode` trong OpenCV thực hiện phép toán **erosion** (mài mòn) lên ảnh nhị phân hoặc mặt nạ (mask). Phép mài mòn sẽ làm nhỏ lại các đối tượng sáng (trắng) trong ảnh, giúp loại bỏ các vùng sáng nhỏ hoặc làm giảm kích thước các đối tượng sáng.

```python
   eroded = cv2.erode(mask, kernel, iterations=1)
```
#### **Giải thích tham số**
- `mask`: Ảnh đầu vào (thường là ảnh nhị phân), nơi bạn muốn thực hiện phép mài mòn.
- `kernel`: Ma trận kernel (hoặc structuring element) dùng để mài mòn. Kernel này xác định kích thước và hình dạng của vùng ảnh mà phép mài mòn sẽ áp dụng.
- `iterations`: Số lần phép mài mòn được thực hiện. Mỗi lần phép mài mòn sẽ làm giảm kích thước của các đối tượng sáng trong ảnh. Số lần lặp lại (iterations) càng lớn, hiệu ứng mài mòn càng mạnh.

#### **Cách hoạt động**
Phép toán **erosion** sẽ áp dụng kernel lên từng pixel của ảnh:
- Với mỗi **pixel** trong ảnh, nếu tất cả các pixel trong vùng của kernel có giá trị 255 (trắng), pixel trung tâm sẽ giữ nguyên giá trị 255. Nếu không, pixel trung tâm sẽ được gán giá trị 0 (đen).
- Điều này có nghĩa là một pixel sáng (trắng) sẽ chỉ được giữ lại nếu tất cả các pixel xung quanh nó cũng sáng. Nếu có một pixel nào đó trong vùng kernel có giá trị tối (đen), pixel trung tâm sẽ bị xóa (biến thành đen).

#### **Ứng dụng**
1. **Loại bỏ nhiễu**: Erosion có thể giúp loại bỏ các nhiễu nhỏ trong ảnh, như những vùng sáng nhỏ không mong muốn.
2. **Giảm kích thước của đối tượng sáng**: Dùng để làm nhỏ lại các đối tượng sáng trong ảnh, làm mảnh hơn hoặc xóa bỏ các chi tiết nhỏ.
3. **Phát hiện biên**: Có thể giúp loại bỏ các biên hoặc đối tượng nhỏ trong ảnh mà không phải là đối tượng chính.
4. **Kết hợp với dilation**: Erosion thường được kết hợp với dilation để làm sạch hoặc làm rõ các đối tượng trong ảnh.


## **Smoothing Images | Blurring Images OpenCV**
### **cv2.filter2D**
Hàm `cv2.filter2D` trong OpenCV là một hàm lọc ảnh (convolution filter), cho phép áp dụng một bộ lọc (kernel) lên ảnh đầu vào. Bộ lọc này sẽ được "trượt" qua ảnh, thực hiện phép toán **convolution** (tích chập) tại mỗi pixel của ảnh.

```python
dst = cv2.filter2D(src, ddepth, kernel)
```
#### **Giải thích tham số**
- `src`: Ảnh đầu vào mà bạn muốn áp dụng bộ lọc.
- `ddepth`: Độ sâu của ảnh đầu ra. Thông thường, giá trị `-1` được sử dụng, có nghĩa là độ sâu của ảnh đầu ra sẽ giống với ảnh đầu vào.
- `kernel`: Bộ lọc (kernel) dùng để áp dụng vào ảnh. Kernel này là một ma trận 2D, thường được dùng để làm mờ ảnh, phát hiện biên, hoặc các phép toán xử lý ảnh khác.

#### **Cách hoạt động**
Hàm `filter2D` thực hiện phép toán **convolution** giữa ảnh đầu vào và kernel, tại mỗi pixel trong ảnh, giá trị của pixel đó sẽ được thay thế bằng tổng của các pixel xung quanh nó được nhân với các giá trị tương ứng trong kernel.

Ví dụ đơn giản: nếu bạn có một kernel 3x3, thì tại mỗi pixel của ảnh, giá trị pixel đó sẽ là tổng của các giá trị pixel trong vùng lân cận của nó (3x3), với mỗi pixel được nhân với giá trị tương ứng trong kernel.

#### **Ứng dụng**
- **Làm mờ ảnh**: Áp dụng các bộ lọc như Gaussian blur hoặc mean blur để làm mờ ảnh.
- **Phát hiện biên**: Áp dụng các bộ lọc như Sobel hoặc Laplacian để phát hiện biên trong ảnh.
- **Lọc ảnh với bộ lọc tùy chỉnh**: Bạn có thể tạo ra bất kỳ bộ lọc nào để xử lý ảnh theo nhu cầu của mình.

### **cv2.blur()**
Hàm `cv2.blur()` trong OpenCV là một hàm đơn giản dùng để làm mờ ảnh bằng cách áp dụng bộ lọc trung bình (mean filter) lên ảnh. Khi bạn gọi hàm này, một kernel có kích thước được xác định (ví dụ, 5x5) sẽ được áp dụng lên từng pixel trong ảnh, thay thế giá trị của pixel đó bằng giá trị trung bình của các pixel trong vùng xung quanh nó.

### **cv2.GaussianBlur()**
Hàm `cv2.GaussianBlur()` trong OpenCV được sử dụng để làm mờ ảnh bằng bộ lọc Gaussian, giúp làm mờ ảnh một cách tự nhiên hơn so với bộ lọc trung bình (mean filter) trong cv2.blur(). Bộ lọc Gaussian ưu tiên các pixel gần trung tâm hơn, giúp giảm nhiễu và làm mờ các chi tiết mà không làm mất quá nhiều các biên sắc nét.

### **cv2.medianBlur**
Hàm `cv2.medianBlur(img, 5)` trong OpenCV được sử dụng để áp dụng bộ lọc Median Blur lên ảnh, giúp làm mờ ảnh và loại bỏ nhiễu, đặc biệt là nhiễu muối và tiêu (salt and pepper noise).
( ví dụ kernel = (3x3) thì tại vị trí diểm ảnh trung tâm sẽ lấy ra 9 điểm ảnh xung quang và nó, sau đó sắp xếp theo thứ tự và lấy phần tử ở giữa thay cho phần tử trung tâm)

### **cv2.bilateralFilter**
Hàm `cv2.bilateralFilter` trong OpenCV được sử dụng để áp dụng bộ lọc Bilateral Filter lên ảnh. Đây là một kỹ thuật lọc mạnh mẽ trong xử lý ảnh, giúp làm mờ ảnh mà vẫn giữ lại các cạnh sắc nét. Bộ lọc Bilateral rất hiệu quả trong việc làm mờ ảnh mà không làm mất đi các biên (edges).
#### **Công thức và cách hoạt động của Bilateral Filter:**
Bộ lọc Bilateral sử dụng một phương pháp khác biệt so với các bộ lọc như **Gaussian Blur**. Nó không chỉ dựa vào khoảng cách không gian mà còn dựa vào sự tương đồng của cường độ pixel (tức là giá trị màu sắc của các pixel). Điều này giúp bộ lọc giữ lại các cạnh trong ảnh, giúp làm mờ các vùng có màu tương tự mà không làm mờ các biên rõ ràng.
Công thức của Bilateral Filter:

$$
I(x) = \frac{1}{W_p} \sum_{q \in \Omega} I(q) \cdot \exp \left( -\frac{|I(p) - I(q)|^2}{2\sigma_r^2} \right) \cdot \exp \left( -\frac{|x - q|^2}{2\sigma_d^2} \right)
$$
- I(p): Giá trị pixel tại điểm p.
- I(q): Giá trị pixel tại điểm q.
- Ω: Một vùng lân cận của pixel p.
- σd: Kích thước cửa sổ không gian (hoặc độ rộng của vùng lân cận).
- σr: Khoảng cách màu sắc giữa các pixel.
- Wp: Hệ số chuẩn hóa để đảm bảo tổng trọng số là 1.

## **Image Gradients and Edge Detection**
### **cv2.Laplacian**
Hàm `cv2.Laplacian` trong OpenCV được sử dụng để tính toán Laplacian của ảnh. Laplacian là một bộ lọc vi phân bậc hai, giúp phát hiện biên (edges) trong ảnh.

### **Laplacian là gì?**
Laplacian là một toán tử vi phân bậc hai, được định nghĩa là sự kết hợp của các đạo hàm bậc nhất theo các chiều không gian trong ảnh. Nó đo lường sự thay đổi cường độ của một ảnh. Bộ lọc Laplacian thường được sử dụng để phát hiện các biên, bởi vì nó có thể phát hiện sự thay đổi mạnh mẽ trong cường độ pixel.

Công thức Laplacian trong không gian 2D:
$$
\Delta f(x, y) = \frac{\partial^2 f(x, y)}{\partial x^2} + \frac{\partial^2 f(x, y)}{\partial y^2}
$$
$$
\text{Ở đây, } f(x, y) \text{ là giá trị cường độ của pixel tại điểm } (x, y).
$$