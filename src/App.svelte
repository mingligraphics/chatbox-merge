<script>
  const allMessages = [
    { sender: 'wsj', text: 'Hello, can you send nitazenes to Europe?' },
    { sender: 'dealer', text: 'Hello friend yes how much do you need?' },
    { sender: 'wsj', text: 'To the UK as well? Can you clear customs?' },
    { sender: 'dealer', text: 'Yes, we can ship to the UK. We offer door-to-door delivery with double customs clearance and tax included' },
    { sender: 'wsj', text: 'What is the max quantity you can send?' },
    { sender: 'dealer', text: 'It depends on your needs. We use disguised packaging, which is very safe. Large quantities can be shipped.' },
    { sender: 'wsj', text: 'Kilos?' },
    { sender: 'dealer', text: 'Yes' },
    { sender: 'dealer', image: 'https://images.wsj.net/im-08677925' },
    { sender: 'wsj', text: 'I am a reporter with The Wall Street Journal and I reached out to you because I am writing a story about nitazenes. Would you mind if I ask you a few additional questions?' },
    { sender: 'dealer', text: 'Ok' },
    { sender: 'wsj', text: 'Nitazenes are a highly potent and dangerous type of opioid. It has killed hundreds of people in Europe. Do you have any reservations about selling these drugs, given how dangerous they are?' },
    { sender: 'dealer', text: 'We are a legitimate manufacturer and only work with licensed pharmaceutical companies. The dangers you mentioned are the result of misuse and abuse by individuals, not the product itself. ' },
    { sender: 'dealer', text: 'This question shouldn’t be directed at me. You should be asking how your own country is managing this issue. Why can’t your country control the misuse of drugs?'},
  ];

  let messages = allMessages;
</script>

<div class="chat-container">
  <div class="messages">
    {#each messages as msg, i (msg.text)}
      {#if i === 0}
        <div class="label wsj-label">WSJ reporter</div>
      {/if}
      {#if i === 1}
        <div class="label dealer-label">Nitazenes seller in China</div>
      {/if}
      <div class="message {msg.sender} {msg.text === 'IsotonitazeneProtonitazeneMetonitazeneEtonitazene' ? 'bullet-bubble' : ''}">
        {#if msg.text === 'IsotonitazeneProtonitazeneMetonitazeneEtonitazene'}
          {@html `
            <div class="bullet-list">
              <div>• Isotonitazene</div>
              <div>  • Protonitazene</div>
              <div>  • Metonitazene</div>
              <div>  • Etonitazene</div>
            </div>
          `}
        {:else if msg.image}
          <!-- svelte-ignore a11y-img-redundant-alt -->
          <img src={msg.image} alt="Photo of protonitazene powder" class="bubble-image" />
        {:else}
          {msg.text}
        {/if}
      </div>
    {/each}
  </div>
</div>

<style>
  .chat-container {
    width: 100%;
    max-width: 450px;
    margin: auto;
    border-radius: 12px;
    padding: 1rem 1.5rem 1rem 0.5rem;
    font-family: Retina, sans-serif;
    font-size: 15px;
    display: flex;
    flex-direction: column;
    background: white;
  }

  .messages {
    display: flex;
    flex-direction: column;
    gap: 0.1rem;
  }

  .message {
    margin: 0.5rem 0;
    max-width: 80%;
    padding: 0.3rem 0.6rem;
    border-radius: 6px;
    line-height: 1.6;
    display: inline-block;
    word-wrap: break-word;
    white-space: pre-wrap;
  }

  .message.bullet-bubble {
    margin: 0 !important;
    padding: 0.05rem 0.3rem !important;
    line-height: 0.5 !important;
  }

  .bullet-list {
    margin: 0;
    padding: 0;
    line-height: 0.5;
  }

  .bubble-image {
    width: 200px;
    height: auto;
    border-radius: 6px;
    display: block;
  }

  .label {
    font-size: 13px;
    font-weight: bold;
    margin-bottom: 0.2rem;
    font-family: Retina, sans-serif;
  }

  .wsj-label {
    text-align: right;
    margin-right: 0.6rem;
  }

  .dealer-label {
    text-align: left;
    margin-left: 0.6rem;
  }

  .wsj {
    background-color: #0078FE;
    align-self: flex-end;
    color: white;
  }

  .dealer {
    background-color: #E5E5EA;
    align-self: flex-start;
  }
</style>
