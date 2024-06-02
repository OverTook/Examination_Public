> [!IMPORTANT]
>
> 이하 내용은 모두 Private Repositroy로 등록되어 있는 프로젝트에 관한 설명입니다. 
>
> 열람이 필요한 경우 요청바랍니다.

<br>

# 시험 관리 시스템 (EMS)

![Examination_1](./Examination_1.png)

[시험 관리 시스템](https://github.com/OverTook/Examination) 은 C# 클라이언트와 PHP 서버를 이용하여 구동되는 시험 관리 프로그램입니다.

> [!NOTE]
>
> PHP 기반 서버는 이후 Go언어로 Conversion이 이루어질 예정입니다.
> 

<br>

본 시험 관리 시스템은 기존의 다양한 기관에서 사용 중에 있는 LMS의 시험 부정 행위를 방지하기 위하여 개발된 단기 프로젝트 입니다.

따라서 부정 행위를 방지하고자 하는 만큼 주요 기능은 다음과 같습니다.

1. [Alt + Tab], [Alt + F4], [Ctrl + Alt + Del] 등 다양한 Key Input 제어
2. 주 모니터를 제외한 나머지 모니터를 차단

<br>

이하 게시글에서는 EMS에 관한 전반적인 설명 및 사용 방법을 설명합니다.

<br>


# Getting Started / 어떻게 시작하나요?

좋습니다! 이제 시험 관리 시스템을 설치하고 구동하는 방법에 대해서 설명하도록 하겠습니다.

<br>

## Server / 서버

### Prerequisites / 선행 조건

시험 관리 시스템의 서버를 구동하기 위해서는 아래 조건을 만족해야 합니다.

> APM

만약, APM이 설치되어 있지 않다면 다음 과정을 통해 설치할 수 있습니다.

#### Ubuntu

```shell
sudo apt update
sudo apt install apache2
sudo apache2ctl -v

sudo ufw allow 'Apache'

sudo apt-get install php
sudo apt install mysql-server -y
```

#### Windows

> [!TIP]
>
> Apache, PHP, MySQL 버전은 원하는 버전으로 바꿀 수 있습니다.

PHP 설치

```cmd
curl -o php.zip https://windows.php.net/downloads/releases/php-8.3.7-Win32-vs16-x64.zip
tar -xf php.zip -C C:\php
cd C:\php
copy php.ini-production php.ini

powershell -Command "(Get-Content php.ini) -replace ';extension=pdo_mysql', 'extension=pdo_mysql' | Set-Content php.ini"
```

MySQL 설치

```cmd
curl -o mysql-installer.msi https://dev.mysql.com/get/Downloads/MySQLInstaller/mysql-installer-web-community-8.0.26.0.msi
msiexec /i mysql-installer.msi /quiet
"C:\Program Files\MySQL\MySQL Server 8.0\bin\mysqld" --initialize-insecure
"C:\Program Files\MySQL\MySQL Server 8.0\bin\mysqld" --install
net start MySQL
```

Apache 설치

```cmd
curl -o httpd.zip https://www.apachelounge.com/download/VS17/binaries/httpd-2.4.59-240404-win64-VS17.zip
tar -xf httpd.zip -C C:\Apache24
cd C:\Apache24\conf
echo LoadModule php_module "c:/php/php7apache2_4.dll" >> httpd.conf
echo AddType application/x-httpd-php .php >> httpd.conf
echo PHPIniDir "c:/php" >> httpd.conf
```

<br>

### Installing / 설치

해당 Repository의 최신 Release 파일을 내려받아 수동으로 파일을 이동하거나, 아래 명령어를 통해 설치할 수 있습니다.

#### Ubuntu

```shell
git clone https://github.com/OverTook/Examination.git /tmp/Examination
sudo cp -r /tmp/Examination/PHPServer/* /var/www/html/
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
sudo systemctl restart apache2
```

#### Windows

```cmd
git clone https://github.com/OverTook/Examination.git C:\TEMP_DIR\Examination
xcopy C:\TEMP_DIR\Examination\PHPServer\* C:\Apache24\htdocs /E /H /Y
```

<br>

## Client / 클라이언트

> [!CAUTION]
>
> Windows 환경 이외에는 클라이언트를 실행할 수 없습니다.

### Prerequisites / 선행 조건

시험 관리 시스템의 클라이언트를 구동하기 위해서는 아래 조건을 만족해야 합니다.

> C# 8.0

Windows 환경을 만족하면서 C#이 설치되어 있지 않다면 명령 프롬프트에서 아래 명령어를 통해 설치할 수 있습니다.

```cmd
winget install Microsoft.DotNet.SDK.8
```

<br>

### Installing / 설치

해당 Repository의 최신 Release 파일을 내려받거나, 아래 명령어를 통해 내려받은 후 직접 컴파일을 진행할 수 있습니다.

```cmd
gh repo clone OverTook/Examination
```

<br>



> [!NOTE]
>
> 내용이 추가되고 있습니다. 잠시만 기다려주세요. 2024-06-02

