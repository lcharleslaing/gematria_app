<script context="module">
  let phrase = "";
  // export async function load() {
  //   let { data, error } = await supabase.from("Gematria").select("*");
  //   if (error) {
  //     return { error };
  //   }
  //   return {
  //     props: { data },
  //   };
  // }
</script>

<script>
  import { simple, english, hebrew } from "../files/gematria.js";

  let phrase = "";

  const getGematriaValue = (input) => {
    let sum = 0;
    for (let i = 0; i < input.length; i++) {
      let letter = input[i].toLowerCase();
      let index = simple.findIndex((item) => item.letter === letter);
      if (index !== -1) {
        sum += simple[index].value;
      }
    }

    // insert sum into id of sumId element
    let urlOneBase = `https://qagg.news/?q=%23%23${sum}`;
    document.getElementById("sumId").href = urlOneBase;

    document.getElementById("sumId").innerHTML = sum;

    let letters = input.split("");
    let simple_one_step = [];
    for (let i = 0; i < letters.length; i++) {
      let letter = letters[i];
      let lower = letter.toLowerCase();
      let index = simple.findIndex((item) => item.letter === lower);
      if (index !== -1) {
        simple_one_step.push(simple[index].text);
      }
      if (letter === " ") {
        simple_one_step.push("zero");
      }
    }
    let simple_one_step_string = simple_one_step.join(" ");

    let sum2 = 0;
    for (let i = 0; i < simple_one_step_string.length; i++) {
      let letter = simple_one_step_string[i];
      let lower = letter.toLowerCase();
      let index = simple.findIndex((item) => item.letter === lower);
      if (index !== -1) {
        sum2 += simple[index].value;
      }
    }
    console.log("1-Step Value: ", sum);
    console.log("2-Step Value: ", sum2);
    console.log(letters);
    console.log(simple_one_step);
    console.log("String to 2-Step: ", simple_one_step_string);

    // insert sum into id of sumId element
    document.getElementById("phrase").innerHTML = phrase;

    // insert sum into id of sumId element
    let urlTwoBase = `https://qagg.news/?q=%23%23${sum2}`;
    // add url to href of id sum2Id
    document.getElementById("sum2Id").href = urlTwoBase;
    document.getElementById("sum2Id").innerHTML = sum2;

    // insert sum into id of sumId element
    // document.getElementById("2-step-phrase").innerHTML = simple_one_step_string;

    phrase = "";
  };

  function onEnter(event) {
    if (event.key === "Enter") {
      getGematriaValue(phrase);
    }
  }
</script>

<div class="">
  <div class="text-center text-6xl font-extrabold">Gematria</div>
  <div class="phrase-search text-center text-2xl my-2 mt-6 font-extrabold">
    <!-- {gematria} -->
  </div>
  <div class="text-center my-6">
    <input
      on:keydown={onEnter}
      bind:value={phrase}
      type="text"
      placeholder="Enter your text, press enter or click 'DO IT!'"
      class="input w-full max-w-xs input-bordered input secondary"
    />
    <button
      on:click={getGematriaValue(phrase)}
      id="button"
      class="btn btn-accent">Do It!</button
    >
  </div>

  <!-- ids: sumId, sum2Id, 2-step-phrase, phrase -->
  <div class="text-center my-4 text-4xl font-bold" id="phrase" />
  <div class="text-center flex flex-wrap w-72 m-auto">
    <a
      target="_blank"
      href="/"
      class="card shadow-md m-auto p-3 rounded-xl text-3xl bg-accent text-white"
      id="sumId">1 Step</a
    >
    <a
      target="_blank"
      href="/"
      class="card shadow-md m-auto p-3 rounded-xl text-3xl bg-accent text-white"
      id="sum2Id">2 Step</a
    >
    <div class="card m-2 my-6 p-2 bg-transparent text-slate-500">
      Click on the 1-Step or the 2-Step button to go directly to that Q-Drop.
    </div>
  </div>
  <div class="text-center my-4 text-xl italic" id="2-step-phrase" />
</div>

<style>
</style>
