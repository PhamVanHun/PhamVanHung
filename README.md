# PhamVanHung
Đam mê lập trình

#Mô hình dự đoán thời gian học toán của ngày tiếp theo
import numpy as np
import matplotlib
import matplotlib.pyplot as plt
from sklearn import linear_model

def day_study_math(study_day_math):
	h = [1] #Danh sách gồm số ngày dự kiếm học toán

	for i in range(2,study_day_math+1):
		h.append(i)
	return h

def time_study_math(study_day_math):
	e = [] #Danh sách thời gian học toán qua từng ngày

	for j in range(1,study_day_math+1):
		print("Ngày ",j)
		A = int(input("Thời học toán: "))
		e.append(A)
	return e

def draw_1(list_study_day_math,list_time_study_math):
	#Biến đổi các danh sách thành ma trận và đổi vị trí hàng thành cột 
	A = np.array([list_study_day_math]).T 
	b = np.array([list_time_study_math]).T

	#Vẽ lên đồ thị các điểm dữ liệu đã nhập
	plt.plot(A,b,"ro")
	plt.title("Mô hình dự đoán thời gian học toán cho những ngày tiếp theo")
	plt.xlabel("Ngày học toán")
	plt.ylabel("Thời gian học toán(giờ)")

	#Huấn luyện LinearRegression và từ đó vẽ lên đường thẳng cần dự đoán
	lr = linear_model.LinearRegression()
	lr.fit(A,b)

	x0 = np.array([[1,max(list_study_day_math)]]).T #Random ra các điểm ngẫu nhiên từ 1 đến giá trị lớn nhất trong danh sách gồm số ngày dự kiến học toán
	y0 = x0*lr.coef_ + lr.intercept_ #từ các điểm random ở trên ta xây dựng lên phương trình đường thẳng cần tìm có dạng y = ax + b và từ đó tính ra các giá trị y0

	plt.plot(x0,y0)
	plt.show()
	
def main():
	study_day_math = int(input("Nhập vào số ngày dự kiến học toán: "))#Dữ liệu đầu vào

	list_study_day_math = day_study_math(study_day_math) 
	list_time_study_math = time_study_math(study_day_math)
	
	draw_1(list_study_day_math,list_time_study_math)#Hàm dùng để lưu và sử dụng các giá trị của danh sách gồm ngày học toán và thời gian học toán

main()
#Kết thúc chương trình
