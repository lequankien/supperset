Clone superset cho vmlp tại:  https://github.com/lequankien/supperset/tree/master/superset-frontend
Cài đặt môi trường dev cho superset: yêu cầu python3, nodejs > v20
-	BE: 
o	Cài đặt LDAP:
─# apt-get update -y
	└─# apt-get install build-essential python3-dev python2.7-dev libldap2-dev libsasl2-dev slapd ldap-utils tox lcov valgrind
	
	└─# apt-get update -y
	
  └─# pip install python-ldap
o	Cài đặt môi trường cho superset : chú ý bản mysqlclient 2.2.4 nếu bị lỗi thì có thể thay bẳng phiên bản lớn hơn
	python3 -m venv venv # setup a python3 virtualenv
source venv/bin/activate

pip install -r requirements/development.txt

pip install -e .

superset db upgrade

superset fab create-admin

superset init

superset load-examples

superset run -p 8088 --with-threads --reload --debugger –debug
-	FE: cd vào thư mục superset-frontend
o	 Chỉnh sửa file // package.json
  // ...
  "scarfSettings": {
    "enabled": false
  }
  // ... 
	Sau đó chạy lệnh:  npm ci
	Rồi chạy lệnh: npm run dev-server để start
	Cấu hình thông tin BE ở superset-frontend/webpack.config.js
-	Build image: tại folder superset chạy lệnh
o	Docker build -t name
