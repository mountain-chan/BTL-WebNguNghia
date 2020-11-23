# BTL-WebNguNghia
Đề tài: Mô quản lý đặt phòng khách sạn trên Protoge, sử dụng truy vấn SPARQL query để tìm kiếm dữ liệu


# RDF và rdfs

## rdfs là các rằng buộc, cấu trúc của rdf, rdf là các thể hiện của rdfs
## Mỗi thuộc tính đều có Domain và Range
## Domain: chỉ ra thuộc tính thuộc về lớp nào
## Range : miền giá trị của thuộc tính




# SPARQL query

## Lấy tất cả khách sạn
```bash
PREFIX qlks: <http://people.brunel.ac.uk/~csstnns/QLKS.owl#>
select *  WHERE {
	?KhachSan qlks:TenKhachSan ?Ten.
	?KhachSan qlks:CoGiapBien ?GiapBien.
}
ORDER BY (?Ten) 
```


## Tìm tất cả các khách sạn thuộc một thành phố
```bash
PREFIX qlks: <http://people.brunel.ac.uk/~csstnns/QLKS.owl#>
select *  WHERE {
	?KhachSan qlks:ThuocTP qlks:TP1.
	?KhachSan qlks:TenKhachSan ?TenKhachSan.
	?KhachSan qlks:CoGiapBien ?GiapBien.
}
```

## Tìm các khách sạn có giáp biển
```bash
PREFIX qlks: <http://people.brunel.ac.uk/~csstnns/QLKS.owl#>
select *  WHERE {
	?KhachSan qlks:TenKhachSan ?Ten.
	?KhachSan qlks:CoGiapBien ?GiapBien.
	FILTER (?GiapBien = true)
}
ORDER BY (?Ten) 
```


## Danh sách phòng của một khách sạn
```bash
PREFIX qlks: <http://people.brunel.ac.uk/~csstnns/QLKS.owl#>
select *  WHERE {
	?Phong qlks:ThuocKSan qlks:KS1.
	?Phong qlks:TenPhong ?TenPhong.
	?Phong qlks:DienTich ?DienTich.
	?Phong qlks:GiaThue ?GiaThue.
}
ORDER BY DESC(?GiaThue)
```

## Tìm các phòng có diện tích n
```
PREFIX qlks: <http://people.brunel.ac.uk/~csstnns/QLKS.owl#>
select *  WHERE {
	?Phong qlks:TenPhong ?TenPhong.
	?Phong qlks:DienTich ?DienTich.
	?Phong qlks:GiaThue ?GiaThue.
	FILTER (?DienTich = 25)
}
```

## Tìm các phòng có diện tích > n
```bash
PREFIX qlks: <http://people.brunel.ac.uk/~csstnns/QLKS.owl#>
select *  WHERE {
	?Phong qlks:TenPhong ?TenPhong.
	?Phong qlks:DienTich ?DienTich.
	?Phong qlks:GiaThue ?GiaThue.
	FILTER (?DienTich > 25)
}
order by desc (?DienTich)
```

## Tìm các phòng có diện tích n của khách sạn a
```bash
PREFIX qlks: <http://people.brunel.ac.uk/~csstnns/QLKS.owl#>
select *  WHERE {
	?Phong qlks:ThuocKSan qlks:KS1.
	?Phong qlks:TenPhong ?TenPhong.
	?Phong qlks:DienTich ?DienTich.
	?Phong qlks:GiaThue ?GiaThue.
	FILTER (?DienTich = 25)
}
```

## Tìm thông tin của của phòng a
```bash
PREFIX qlks: <http://people.brunel.ac.uk/~csstnns/QLKS.owl#>
select *  WHERE {
	?Phong qlks:TenPhong ?TenPhong.
	?Phong qlks:DienTich ?DienTich.
	?Phong qlks:GiaThue ?GiaThue.
	FILTER (?TenPhong = "Phong 101")
}
```

## Tìm các phòng đã được đặt vào ngày n
```
PREFIX qlks: <http://people.brunel.ac.uk/~csstnns/QLKS.owl#>
select *  WHERE {
	?DP qlks:NgayDen ?NgayDen.
	?DP qlks:NgayTra ?NgayTra.
	?DP qlks:ThanhTien ?ThanhTien.
	?DP qlks:DaHuy ?DaHuy.
	FILTER (?NgayDen <= "2020-11-22T08:00:00"^^xsd:dateTime && ?NgayTra >= "2020-11-22T08:00:00"^^xsd:dateTime).
}
order by (?NgayDen)
```

## Tìm các đơn đặt phòng đã bị hủy
```
PREFIX qlks: <http://people.brunel.ac.uk/~csstnns/QLKS.owl#>
select *  WHERE {
	?DP qlks:NgayDen ?NgayDen.
	?DP qlks:NgayTra ?NgayTra.
	?DP qlks:ThanhTien ?ThanhTien.
	?DP qlks:DaHuy ?DaHuy.
	FILTER (?DaHuy = true)
}
```

## Tìm các đặt phòng của khách hàng a
```
PREFIX qlks: <http://people.brunel.ac.uk/~csstnns/QLKS.owl#>
select *  WHERE {
	?DP qlks:ThuocKhachHang ?KH.
	?DP qlks:ThanhTien ?ThanhTien.
	?KH qlks:TenTaiKhoan ?TenTaiKhoan.
	Filter (?TenTaiKhoan = "Khach Hang 1")
}
```

## Tính tổng tiền đặt phòng của khách hàng a
```
PREFIX qlks: <http://people.brunel.ac.uk/~csstnns/QLKS.owl#>
select  ?TenTaiKhoan  (SUM(?ThanhTien) as ?TongTien)   WHERE {
	?DP qlks:ThuocKhachHang ?KH.
	?DP qlks:ThanhTien ?ThanhTien.
	?KH qlks:TenTaiKhoan ?TenTaiKhoan.
	Filter (?TenTaiKhoan = "Khach Hang 1")
}
group by ( ?TenTaiKhoan)
```


