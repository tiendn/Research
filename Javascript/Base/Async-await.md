## Hiểu rõ Promises trước khi bạn bắt đầu sử dụng async/await.
Với Babel ngày nay hỗ trợ async/await ra ngoài khuôn khổ ( ý ở đây ám chỉ các trình duyệt cũ ), và ES2016(ES7) đã phổ biến quanh đâu đó đây, nhiều và nhiều người nhận ra sự tuyệt vời như thế nào của việc viết asynchronous code, sử dụng cấu trúc synchronous code.

Đó là một điều tốt và nâng cao chất lượng mã/code lên nhiều.

Tuy nhiên, vẫn nhiều người xiên hổng rằng toàn bộ nền tảng của async/await là **Promises**. Thực tế, **mỗi hàm async bạn viết sẽ trở thành một Promise, và mọi thứ bạn await sẽ là một promise.**

Tại sao tôi nhấn mạnh điều đó? Bởi vì phần chính của javascript viết ngày nay sử dụng callback; rất nhiều người thiếu mảnh ghép chính của async/await.

Promise là gì ?
Tôi sẽ giữ điều ngắn gọn này, từ khi nó được bao phủ rộng rãi ở nơi khác.

Một promise là một phần đặc biệt của javascript object bao gồm object khác. Tôi có một promise cho số nguyên 17 và xâu "Hello monkey!", và vài object tuỳ tiện khác, hoặc những thứ khác bạn có thể lưu một cách bình thường trong biến javascript.

Làm thế nào tôi truy cập tới data trong Promise? Hãy sử dụng `.then()`;

```javascript
  function getFirstUser() {
    return getUsers().then(function(users) {
        return users[0].name;
    });
  }
```

Đó, tôi có thể truy cập tới name của user từ bên trong db hay ở đâu đó bởi fn `getUsers()` thông qua xử lý async.
Tuy nhiên, nếu như chẳng may bạn bị gặp lỗi giữa chừng, bạn xử lý ra sao? **Catch**?
Đúng, và trong js promise chúng ta chỉ cần gọi thêm `.catch()` ngay sau `.then()` kết thúc như sau:

```javascript
  function getFirstUser() {
    return getUsers().then(function(users) {
        return users[0].name;
    }).catch(function(err) {
        return {
          name: 'default user'
        };
    });
}
```

Tóm lại, có một async function, nhưng không có nghĩa là nó trả về data ngay lúc này hay về sau, mà là thông qua `.then()`