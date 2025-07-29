<script>
  import { fade } from 'svelte/transition';
  import { onMount } from 'svelte';

  // All messages (prewritten)
  const allMessages = [
    { sender: 'wsj', text: 'Hello, can you send nitazenes to Europe?' },
    { sender: 'dealer', text: 'Hello friend yes how much do you need?' },
    { sender: 'wsj', text: 'To the UK as well? Can you clear customs?' },
    { sender: 'dealer', text: 'Yes, we can ship to the UK. We offer door-to-door delivery with double customs clearance and tax included' },
    { sender: 'wsj', text: 'And what types of nitazenes do you have?' },
    { sender: 'dealer', text: 'IsotonitazeneProtonitazeneMetonitazeneEtonitazene'},
    { sender: 'wsj', text: 'What is the max quantity you can send?' },
    { sender: 'dealer', text: 'It depends on your needs. We use disguised packaging, which is very safe. Large quantities can be shipped.' },
    { sender: 'wsj', text: 'Kilos?' },
    { sender: 'dealer', text: 'Yes' },
    { sender: 'dealer', image: 'https://images.wsj.net/im-08677925' },
    { sender: 'wsj', text: 'Are you sending them from China?' },
    { sender: 'dealer', text: 'Yes from China'},
    { sender: 'dealer', text: 'We are a factory'},
    { sender: 'wsj', text: 'What’s the kilo price for protonitazene, metonitazene and etonitazene?' },
    { sender: 'dealer', text: 'list of things' },
    { sender: 'wsj', text: 'I am a reporter with The Wall Street Journal and I reached out to you because I am writing a story about nitazenes. Would you mind if I ask you a few additional questions?' },
    { sender: 'dealer', text: 'Ok' },
    { sender: 'wsj', text: 'Nitazenes are a highly potent and dangerous type of opioid. It has killed hundreds of people in Europe. Do you have any reservations about selling these drugs, given how dangerous they are?' },
    { sender: 'dealer', text: 'We are a legitimate manufacturer and only work with licensed pharmaceutical companies. The dangers you mentioned are the result of misuse and abuse by individuals, not the product itself. ' },
    { sender: 'dealer', text: 'This question shouldn’t be directed at me. You should be asking how your own country is managing this issue. Why can’t your country control the misuse of drugs?'},
  ];

  let messages = []; // These will appear one by one

  let index = 0;

  let inView = false;

  // Show messages one at a time with delay
  const showNextMessage = () => {
    if (index < allMessages.length) {
      messages = [...messages, allMessages[index]];
      index++;
      setTimeout(showNextMessage, 1000); // 1 second delay between each
    }
  };

  function handleInView(entry) {
    if (entry.isIntersecting && !inView) {
      inView = true;
      showNextMessage();
    }
  }

  let observer;
  let container;

  // Start on mount
  onMount(() => {
    observer = new IntersectionObserver(([entry]) => handleInView(entry), {
      threshold: 0.2
    });
    if (container) observer.observe(container);

    return () => observer && observer.disconnect();
  });
</script>

<div bind:this={container} class="chat-container">
  <div class="messages">
    {#each messages as msg, i (msg.text)}
    {#if i === 0}
      <div class="label wsj-label" transition:fade>WSJ reporter</div>
    {/if}
    {#if i === 1}
      <div class="label dealer-label" transition:fade>Nitazene seller</div>
    {/if}
      <div class="message {msg.sender} {msg.text === 'IsotonitazeneProtonitazeneMetonitazeneEtonitazene' ? 'bullet-bubble' : ''}" transition:fade>
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
    /* border: 1px solid #ccc; */
    border-radius: 12px;
    padding: 1rem 1.5rem 1rem 0.5rem; /* Less left, more right */
    font-family: Retina, sans-serif;
    font-size: 15px;
    display: flex;
    flex-direction: column;
    background: white;
    /* box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05); */
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
  margin: 0 !important;        /* remove top & bottom margin */
  padding: 0.05rem 0.3rem !important;  /* reduce padding inside bubble */
  line-height: 0.5 !important;
}

.bullet-list {
  margin: 0;            /* remove margin around bullet list */
  padding: 0;           /* remove padding */
  line-height: 0.5;     /* tighten line height inside bullet list */
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


