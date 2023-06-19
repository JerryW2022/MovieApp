# 1 fetch()
`fetch()` 是 JavaScript 的一个内置函数，用于发送 HTTP 请求并获取响应。它提供了一种现代的方式来执行网络请求，并且在大多数现代浏览器中都得到了广泛支持。

基本用法如下：

```javascript
fetch(url)
  .then(response => {
    // 处理响应
  })
  .catch(error => {
    // 处理错误
  });
```

上述代码中，`fetch(url)` 发起了一个 GET 请求，并返回一个 Promise 对象。可以通过 `.then()` 方法来处理成功的响应，并通过 `.catch()` 方法来处理错误。

在处理响应时，可以使用 `response` 对象来获取响应的信息，如状态码、头部信息等。可以使用 `response.json()`、`response.text()`、`response.blob()` 等方法来处理响应的内容，并将其解析为不同的数据类型。

例如，使用 `response.json()` 方法将响应解析为 JSON 数据：

```javascript
fetch(url)
  .then(response => response.json())
  .then(data => {
    // 处理解析后的 JSON 数据
  })
  .catch(error => {
    // 处理错误
  });
```

在这个例子中，通过使用 `response.json()` 方法，将响应解析为 JSON 数据，并在第二个 `.then()` 中处理解析后的数据。

在 `fetch()` 中还可以传递可选的第二个参数，用于配置请求的方法、头部、身份验证等。例如，可以使用 `fetch(url, options)` 来发送带有自定义配置的请求。

需要注意的是，`fetch()` 默认不会将网络错误（如请求失败、跨域错误等）视为拒绝的 Promise，只有在网络请求无法完成时才会拒绝。如果要处理网络错误，可以使用 `.catch()` 方法来捕获错误并进行相应处理。

# 2 fetch() 的第二种写法
如果你不想使用 `then()` 方法来处理 `fetch()` 的响应，你可以使用 `async/await` 来编写更简洁的异步代码。`async/await` 是 ES2017 引入的语法，用于处理异步操作。

下面是使用 `async/await` 的示例代码：

```javascript
async function fetchData(url) {
  try {
    const response = await fetch(url);
    const data = await response.json();
    // 处理解析后的数据
    return data;
  } catch (error) {
    // 处理错误
    console.error(error);
  }
}

// 调用 fetchData 函数
const result = await fetchData(url);
// 使用返回的数据 result 进行后续操作
```

在上述代码中，我们定义了一个名为 `fetchData` 的异步函数，使用 `async` 关键字来声明该函数为异步函数。

在函数体内部，我们使用 `await` 关键字来等待 `fetch()` 返回的 Promise 对象解析为一个实际的响应对象 `response`，然后再使用 `await` 关键字等待将响应解析为 JSON 数据的 Promise 对象 `response.json()`。

在 `try` 块中，我们可以直接处理解析后的数据，并在函数末尾使用 `return` 语句返回数据。

如果发生错误，`catch` 块将捕获错误，并将错误信息打印到控制台进行处理。

最后，在调用 `fetchData` 函数时，我们可以使用 `await` 关键字等待函数执行完毕，并将返回的数据赋值给变量 `result`，然后使用该变量进行后续操作。

这种使用 `async/await` 的写法可以使异步代码更加简洁和易读，让代码更接近同步的写法风格。