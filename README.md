<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rút Gọn Link</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/sweetalert2@10.16.6/dist/sweetalert2.min.css">
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #fef2f2;
            justify-content: center;
            align-items: center;
            width: auto;
        }
        .container {
            margin: 30% auto;
            width: auto;
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        form {
            margin: 0px auto;
            width: auto;
            padding: 50px;
        }
        
        h2 {
          text-align: center;
          color: #004aad;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
        }
        input[type="text"] {
            width: 100%;
            padding: 8px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            width: 100%;
            padding: 10px 15px;
            background-color: #004aad;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container">
        <form id="shorten-form">
          <h2>ApkS2Life</h2>
          <h6>Công cụ rút gọn link của bạn</h6>
            <div class="form-group">
                <label for="original-link">Link dài:</label>
                <input type="text" id="original-link" name="original-link" required>
            </div>
            <div class="form-group">
                <label for="keyword">Từ khóa:</label>
                <input type="text" id="keyword" name="keyword" required>
            </div>
            <button type="submit">Rút gọn link</button>
        </form>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/sweetalert2@10.16.6/dist/sweetalert2.all.min.js"></script>
    <script>
        document.getElementById('shorten-form').addEventListener('submit', async function(e) {
            e.preventDefault();

            const originalLink = document.getElementById('original-link').value;
            const keyword = document.getElementById('keyword').value;

            const formData = new FormData();
            formData.append('originalLink', originalLink);
            formData.append('keyword', keyword);

            try {
                const response = await fetch('https://script.google.com/macros/s/AKfycbwJgR1iLkDU-Hly1MHRR4kfUFpkmm27kE9bxwxEMFg0_UpV_moIIhSjR1sWLcNXcIR9bg/exec', {
                    method: 'POST',
                    body: formData
                });

                const result = await response.json();

                if (result.success) {
                    Swal.fire({
                        title: 'Thành công!',
                        html: `<span>Link rút gọn của bạn:</span><br>[ <a href="${result.shortLink}" style="text-decoration:none;">${result.shortLink} </a>]`,
                        icon: 'success',
                        confirmButtonText: 'OK'
                    });
                } else {
                    Swal.fire({
                        title: 'Lỗi!',
                        text: result.message,
                        icon: 'error',
                        confirmButtonText: 'OK'
                    });
                }
            } catch (error) {
                Swal.fire({
                    title: 'Lỗi!',
                    text: 'Đã có lỗi xảy ra. Vui lòng thử lại sau.',
                    icon: 'error',
                    confirmButtonText: 'OK'
                });
            }
        });
    </script>
</body>
</html>
