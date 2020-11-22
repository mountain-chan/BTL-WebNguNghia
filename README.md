# BTL-WebNguNghia
Đề tài: Mô quản lý đặt phòng khách sạn trên Protoge, sử dụng truy vấn SPARQL query để tìm kiếm dữ liệu


#SPARQL query

##Lấy tất cả khách sạn
select *  WHERE {
	?KhachSan qlks:TenKhachSan ?Ten.
	?KhachSan qlks:CoGiapBien ?GiapBien.
}
ORDER BY (?Ten) 

1: Tìm tất cả các khách sạn thuộc một thành phố
select *  WHERE {
	?KhachSan qlks:ThuocTP qlks:TP1.
	?KhachSan qlks:TenKhachSan ?TenKhachSan.
	?KhachSan qlks:CoGiapBien ?GiapBien.
}

2: Tìm các khách sạn có giáp biển
select *  WHERE {
	?KhachSan qlks:TenKhachSan ?Ten.
	?KhachSan qlks:CoGiapBien ?GiapBien.
	FILTER (?GiapBien = true)
}
ORDER BY (?Ten) 

3: Danh sách phòng của một khách sạn
select *  WHERE {
	?Phong qlks:ThuocKSan qlks:KS1.
	?Phong qlks:TenPhong ?TenPhong.
	?Phong qlks:DienTich ?DienTich.
	?Phong qlks:GiaThue ?GiaThue.
}
ORDER BY DESC(?GiaThue)


4: Tìm các phòng có diện tích n
select *  WHERE {
	?Phong qlks:TenPhong ?TenPhong.
	?Phong qlks:DienTich ?DienTich.
	?Phong qlks:GiaThue ?GiaThue.
	FILTER (?DienTich = 25)
}

4: Tìm các phòng có diện tích > n
select *  WHERE {
	?Phong qlks:TenPhong ?TenPhong.
	?Phong qlks:DienTich ?DienTich.
	?Phong qlks:GiaThue ?GiaThue.
	FILTER (?DienTich > 25)
}
order by desc (?DienTich)

4: Tìm các phòng có diện tích n của khách sạn a
select *  WHERE {
	?Phong qlks:ThuocKSan qlks:KS1.
	?Phong qlks:TenPhong ?TenPhong.
	?Phong qlks:DienTich ?DienTich.
	?Phong qlks:GiaThue ?GiaThue.
	FILTER (?DienTich = 25)
}


5: Tìm thông tin của của phòng a
select *  WHERE {
	?Phong qlks:TenPhong ?TenPhong.
	?Phong qlks:DienTich ?DienTich.
	?Phong qlks:GiaThue ?GiaThue.
	FILTER (?TenPhong = "Phong 101")
}

6: Tìm các phòng đã được đặt vào ngày n
select *  WHERE {
	?DP qlks:NgayDen ?NgayDen.
	?DP qlks:NgayTra ?NgayTra.
	?DP qlks:ThanhTien ?ThanhTien.
	?DP qlks:DaHuy ?DaHuy.
	FILTER (?NgayDen <= "2020-11-22T08:00:00"^^<http://www.w3.org/2001/XMLSchema#dateTime> && ?NgayTra >= "2020-11-22T08:00:00"^^<http://www.w3.org/2001/XMLSchema#dateTime>)
}
order by (?NgayDen)


8: Tìm các đơn đặt phòng đã bị hủy
select *  WHERE {
	?DP qlks:NgayDen ?NgayDen.
	?DP qlks:NgayTra ?NgayTra.
	?DP qlks:ThanhTien ?ThanhTien.
	?DP qlks:DaHuy ?DaHuy.
	FILTER (?DaHuy = true)
}

