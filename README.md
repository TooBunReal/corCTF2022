## corCTF2022
# jsonquiz
Link Challenge: ```https://jsonquiz.be.ax/```

![image](https://user-images.githubusercontent.com/89735990/184584979-7e4d764d-c4a3-4b93-818c-158ce02d3ef4.png)

- Đại khái thì trang web này là một bộ câu hỏi về Json.
- Mình thử tìm tài liệu trên mạng thì mình thấy được đáp án ở link này: 

         https://ebazhanov.github.io/linkedin-skill-assessments-quizzes/json/json-quiz.html
- Sau khi mình trả lời hết tất cả các câu hỏi thì mình lại nhận được kết quả là dưới 30% số điểm dù mình đã lấy toàn bộ đáp án của bộ đề để trả lời.

![image](https://user-images.githubusercontent.com/89735990/184585681-c024f6a2-64d5-479b-8bc0-bb44d4831010.png)

- Check sơ thì mình phát hiện một Request Method là `POST` và có tên là `submit`.

![image](https://user-images.githubusercontent.com/89735990/184586024-a70c9f62-3fef-46c6-8725-0bdbe5bbcc30.png)

- Cái Request `POST` này sẽ gửi `score: "0"` lên trên server, chính điều này làm cho điểm của mình lúc nào cũng dưới 30%.
- Tới đây có nhiều cách để thay đổi giá trị của `score` nhưng mình chọn Burp Suite cho tiện.
- Mình gửi một Resqest khác có giá trị `score=1000000000` lên server và đây là kết quả:

![image](https://user-images.githubusercontent.com/89735990/184586745-9526ee09-30c5-43b2-b63a-17027a69e51a.png)

Flag: `corctf{th3_linkedin_JSON_quiz_is_too_h4rd!!!}`

# msfrog-generator
Link Challenge: ```https://msfrog-generator.be.ax```

![image](https://user-images.githubusercontent.com/89735990/184587038-d4ff6c2e-f407-48c7-a04a-d16063007034.png)

- Web này cho phép ta tạo con một Ếch từ những icon có sẵn và Generate ra một tấm ảnh.
- Đọc qua Source code thì mình không thấy có gì đặt biệt.
- Mình thử kiểm tra phản hồi của server khi Generate tấm ảnh thì minh phát hiện một thứ.

![image](https://user-images.githubusercontent.com/89735990/184587658-0df34458-9ac1-4955-95f8-afadf1167b14.png)

- Có vẻ như với một mỗi tấm ảnh hoặc một tọa độ x và y khác nhau server sẽ phản hồi một kết quả khác nhau ( trong trường hợp này là một đoạn mã hóa của tấm ảnh ).
- Mình nãy ra một ý định đó là thử rce cái tên file và cái tọa độ bằng ``/etc/passwd``:

![image](https://user-images.githubusercontent.com/89735990/184589089-4a7472d6-6894-45f0-94d1-ba7683deaffc.png)

- Đúng như mình nghĩ, nó là shell. Và ở đây mình sẽ bypass shell bằng `;` và thực hiện Command Injection.

![image](https://user-images.githubusercontent.com/89735990/184589737-026a620c-026b-4b55-a9cb-779956b7283b.png)

![image](https://user-images.githubusercontent.com/89735990/184590207-1311f619-8121-4383-8af2-179fddf218c5.png)

![image](https://user-images.githubusercontent.com/89735990/184590364-4b798b47-105d-44c4-821a-3be69b29b52d.png)

- Sau 7749 lần mò thì mình đã tìm được flag bằng Command ``;cd ../;ls -l; cat * ;/etc/``

Flag: `corctf{sh0uld_h4ve_r3nder3d_cl13nt_s1de_:msfrog:}`


