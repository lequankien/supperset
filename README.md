Clone superset cho vmlp tại:  https://github.com/lequankien/supperset/tree/master/superset-frontend
Cài đặt môi trường dev cho superset 
-	BE: 
o	Cài đặt LDAP:
	─# apt-get update -y
	└─# apt-get install build-essential python3-dev python2.7-dev libldap2-dev libsasl2-dev slapd ldap-utils tox lcov valgrind
	
	└─# apt-get update -y
	
	└─# pip install python-ldap
o	Cài đặt môi trường cho superset : chú ý bản mysqlclient 2.2.4 nếu bị lỗi thì có thể thay bẳng phiên bản lớn hơn
	python3 -m venv venv # setup a python3 virtualenv
source venv/bin/activate

# Install external dependencies
pip install -r requirements/development.txt

# Install Superset in editable (development) mode
pip install -e .

# Initialize the database
superset db upgrade

# Create an admin user in your metadata database (use `admin` as username to be able to load the examples)
superset fab create-admin

# Create default roles and permissions
superset init

# Load some data to play with.
# Note: you MUST have previously created an admin user with the username `admin` for this command to work.
superset load-examples

# Start the Flask dev web server from inside your virtualenv.
# Note that your page may not have CSS at this point.
# See instructions below how to build the front-end assets.
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
