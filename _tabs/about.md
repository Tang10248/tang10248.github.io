---
# the default layout is 'page'
icon: fas fa-info-circle
order: 5
---

> `今度は今度、今は今`{: .language-xx }

<!-- {% include embed/audio.html src='/assets/audio/fdf.mp3' %}    -->


# GPT 对话框示例

以下是一个简单的对话框，允许与 GPT 对话。

<div id="chat-container">
  <div id="chat-box" style="border: 1px solid #ddd; padding: 10px; height: 300px; overflow-y: scroll;">
    <p><strong>系统:</strong> 你好！有什么可以帮助您的吗？</p>
  </div>
  <input id="user-input" type="text" placeholder="输入你的问题..." style="width: calc(100% - 110px); margin-top: 10px;">
  <button id="send-button" style="width: 100px; margin-top: 10px;">发送</button>
</div>

<script>
  const chatBox = document.getElementById('chat-box');
  const userInput = document.getElementById('user-input');
  const sendButton = document.getElementById('send-button');

  sendButton.addEventListener('click', async () => {
    const userMessage = userInput.value.trim();
    if (!userMessage) return;

    // 显示用户输入
    const userMsgHtml = `<p><strong>用户:</strong> ${userMessage}</p>`;
    chatBox.innerHTML += userMsgHtml;

    // 清空输入框
    userInput.value = '';

    // 显示等待消息
    chatBox.innerHTML += `<p><strong>系统:</strong> 正在生成回复...</p>`;
    chatBox.scrollTop = chatBox.scrollHeight;

    try {
      const apiKey = 'sk-aBPsZiSMvw9mUjkieKLz6OWKViMaIiCvXNlYb6B6PLfvG7T1'; // 请替换为你的实际 API Key
      // 调用 OpenAI API
      const response = await fetch('https://www.DMXapi.com/v1/', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Authorization': `Bearer ${apiKey}`, // 替换为你的 API Key
        },
        body: JSON.stringify({
          model: 'gpt-4o',
          messages: [{ role: 'user', content: userMessage }],
        }),
        // 添加 mode: 'cors' 以启用跨域请求
        mode: 'cors'
      });
      console.log(response)
      const data = await response.json();
      const gptReply = data.choices[0]?.message?.content || 'GPT 未能生成回复。';
      
      // 显示 GPT 回复
      chatBox.innerHTML += `<p><strong>系统:</strong> ${gptReply}</p>`;
    } catch (error) {
      chatBox.innerHTML += `<p><strong>系统:</strong> 请求失败，请检查网络或 API 配置。</p>`;
      console.error('Error:', error);
    }

    chatBox.scrollTop = chatBox.scrollHeight; // 滚动到最新
  });
</script>
