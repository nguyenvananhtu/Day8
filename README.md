<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="Day8.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"
        integrity="sha512-iecdLmaskl7CVkqkXNQ/ZH/XLlvWZOJyj7Yy7tcenmpD1ypASozpmT/E0iPtmFIB46ZmdtAc9eNBvH0H/ZpiBw=="
        crossorigin="anonymous" referrerpolicy="no-referrer" />
    <title>Day8</title>
</head>
    <style>
        
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: 'Poppins', sans-serif;
}

body {
	background-image: url(https://haycafe.vn/wp-content/uploads/2022/01/Hinh-nen-vu-tru-khong-gian-sao-tho-vo-cung-ky-vi.jpg);
	background-repeat: no-repeat;
	background-size: cover;
	height: 100vh;
	overflow: hidden;
}

.container {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	width: 400px;
	background-color: rgba(170, 159, 159, 0.3);
	border-radius: 10px;
	box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.05);
}

.container h1 {
	text-align: center;
	padding-top: 20px;
    color: #e0dddd;
}

.container form {
	padding: 0 40px;
}

form .form-control {
	position: relative;
	border-bottom: 2px solid #b9b5b5;
	margin: 40px 0;
}

.form-control.success {
	border-bottom-color: #0c2738;
}

.form-control.error {
	border-bottom-color: #e74c3c;
}

.form-control input {
	width: 100%;
	height: 40px;
	font-size: 16px;
	border: none;
	background: none;
	outline: none;
}

small {
	position: absolute;
	left: 0;
	top: 100%;
	margin-top: 3px;
	color: #f8f5f5;
}

.form-control span::before {
	content: '';
	position: absolute;
	top: 40px;
	left: 0;
	width: 0%;
	height: 2px;
	background: #f3f4f5;
	transition: 0.3s;
}

.form-control input:focus ~ span::before {
	width: 100%;
}

input[type='submit'] {
	margin-top: 20px;
	width: 100%;
	height: 50px;
	border: 1px solid;
	background-color: rgba(39, 33, 33, 0.3);
	border-radius: 25px;
	font-size: 18px;
	color: #f8f6f6;
	font-weight: 700;
	cursor: pointer;
	outline: none;
	transition: 0.5s;
}

input[type='submit']:hover {
	background-color: #1c1c1d;
}

.signup_link {
	margin: 15px 0;
	text-align: center;
	font-size: 16px;
	color: rgb(43, 39, 39);
}

.signup_link a {
	color: #eef2f5;
	text-decoration: none;
}

.signup_link a:hover {
	text-decoration: underline;
}
.form-control input>::placeholder{
    color: #000000;
}
::-webkit-input-placeholder { /* Edge */
  color: rgb(226, 224, 224);
}

:-ms-input-placeholder { /* Internet Explorer */
  color: rgb(216, 210, 210);
}

::placeholder {
  color: rgb(223, 221, 221);
}
    </style>
<body>

    <div class="container">
        <h1>Đăng ký</h1>
        <form>
            <div class="form-control">
                <input type="text" id="username" placeholder="Tên đăng nhập" />
                <span></span>
                <small></small>
</div>
            <div class="form-control">
                <input type="email" id="email" placeholder="Email" />
                <span></span>
                <small></small>
            </div>
            <div class="form-control">
                <input type="password" id="password" placeholder="Mật khẩu" />
                <span></span>
                <small></small>
            </div>
            <div class="form-control">
                <input type="password" id="password2" placeholder="Nhập lại mật khẩu" />
                <span></span>
                <small></small>
            </div>
            <input type="submit" value="Đăng kí" />
            <div class="signup_link">  <a href="#">Bạn đã có tài khoản ?</a> <a href="#">Đăng nhập</a></div>
        </form>
    </div>

    <script>
        const form = document.querySelector('form')
        const username = document.getElementById('username')
        const email = document.getElementById('email')
        const password = document.getElementById('password')
        const password2 = document.getElementById('password2')

      
        function showError(input, message) {
            const formControl = input.parentElement
            formControl.className = 'form-control error'
            const small = formControl.querySelector('small')
            small.innerText = message
        }

       
        function showSuccess(input) {
            const formControl = input.parentElement
            formControl.className = 'form-control success'
            const small = formControl.querySelector('small')
            small.innerText = ''
        }

      
        function checkEmail(input) {
            const re =
                /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/

            if (re.test(input.value.trim())) {
                showSuccess(input)
            } else {
                showError(input, 'Email không hợp lệ')
            }
        }

       
        function checkRequired(inputArr) {
            let isRequired = false
            inputArr.forEach(function (input) {
                if (input.value.trim() === '') {
                    showError(input, ` không được để trống`)
                    isRequired = true
                } else {
                    showSuccess(input)
                }
            })

            return isRequired
        }

        function checkLength(input, min, max) {
            if (input.value.length < min) {
                showError(
                    input,
                    `${getFieldName(input)} phải có ít nhất ${min} ký tự`
                )
            } else if (input.value.length > max) {
                showError(
                    input,
                    `${getFieldName(input)} phải ít hơn ${max} ký tự`
                )
            } else {
showSuccess(input)
            }
        }

        
        function checkPasswordsMatch(input1, input2) {
            if (input1.value !== input2.value) {
                showError(input2, 'Mật khẩu không đúng')
            }
        }

       
        function getFieldName(input) {
            return input.id.charAt(0).toUpperCase() + input.id.slice(1)
        }

      
        form.addEventListener('submit', function (e) {
            e.preventDefault()

            if (!checkRequired([username, email, password, password2])) {
                checkLength(username, 3, 15)
                checkLength(password, 6, 25)
                checkEmail(email)
                checkPasswordsMatch(password, password2)
            }
        })

    </script>


</body>

</html>
