<script>
  import RestService from "$services/rest.js";
  import ToastService from "$services/toast";
  import { Translate, TranslateApiMessage } from "$services/language.js";
  import { navigate } from "svelte-navigator";
  import Input from "$components/Form/Input.svelte";
  import Select from "$components/Form/Select.svelte";


  let values = [
    { key: "lang", customValue: null },
    { key: "form_header", customValue: null },
    { key: "form_text", customValue: null },
    { key: "treatment_spot", customValue: null },
    { key: "treatment_header", customValue: null },
    { key: "review_spot", customValue: null },
    { key: "review_header", customValue: null },
    { key: "map_spot", customValue: null },
    { key: "map_header", customValue: null },
    { key: "map_box_header", customValue: null },
    { key: "map_box_desc", customValue: null },
  ];

  let home = {};
  let langs = [];


  values.map((v) => {
    if (v.defaultValue) {
      home[v.key] = { value: v.defaultValue };
    } else {
      home[v.key] = {};
    }
  });
  const getLang = async () => {
    let response = await RestService.getLangs(undefined, undefined);
    langs = response["langs"];
    console.log(langs, "langs");
  };
  getLang();

  const addHome = async () => {
    let data = {};
    values.map((v) => {
      data[v.key] = home[v.key]?.value;
    });
    let response = await RestService.addHome(data);
    if (response["status"]) {
      ToastService.success($Translate("Successfully-completed"));

      navigate("/panel/homes");
    } else {
      ToastService.error($TranslateApiMessage(response.message));
    }
  };
</script>

<div class="flex flex-wrap mt-4 h-screen relative">
  <div class="w-full mb-12 px-2 lg:px-4 ">
    <button
      class="bg-white text-blue-600 hover:text-red-700 mb-2 border rounded font-bold  text-xs px-4 py-2 rounded shadow hover:shadow-lg outline-none focus:outline-none mr-1 "
      type="button"
      on:click={() => {
        navigate("/panel/homes");
      }}
    >
      <i class="fa fa-arrow-left" />
      {$Translate("Back")}
    </button>
    <div
      class="relative flex flex-col min-w-0 break-words w-full mb-6 shadow-lg rounded bg-gray-100"
    >
      <div class="rounded-t mb-0 px-4 py-3 border-0">
        <div class="text-center flex justify-between">
          <h3 class="font-semibold text-lg text-blueGray-700">Anasayfa ekle</h3>
        </div>
      </div>
      <div class="flex-auto px-4 lg:px-10 py-10 pt-0">
        <div class="flex flex-wrap my-4">
          <div class="w-full lg:w-3/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Dil
              </label>
              <Select
                bind:value={home.lang.value}
                bind:isValid={home.lang.isValid}
                values={langs}
                title={"Dil Seçin"}
                valuesKey={"lang"}
                valuesTitleKey={"title"}
                customClass={"w-full"}
              />
            </div>
          </div>
        </div>
        <div class="flex flex-wrap my-4">
          <div class="w-full lg:w-3/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Form Başlık
              </label>
              <Input
                bind:value={home.form_header.value}
                bind:isValid={home.form_header.isValid}
                placeholder={"Form Başlık"}
                required={true}
              />
            </div>
          </div>
          <div class="w-full lg:w-9/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Form Text
              </label>
              <Input
                bind:value={home.form_text.value}
                bind:isValid={home.form_text.isValid}
                placeholder={"Form Text"}
                required={true}
              />
            </div>
          </div>
        </div>
        <div class="flex flex-wrap my-4">
          <div class="w-full lg:w-3/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Tedaviler Spot
              </label>
              <Input
                bind:value={home.treatment_spot.value}
                bind:isValid={home.treatment_spot.isValid}
                placeholder={"Tedaviler Spot"}
                required={true}
              />
            </div>
          </div>
          <div class="w-full lg:w-9/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Tedaviler Başlık
              </label>
              <Input
                bind:value={home.treatment_header.value}
                bind:isValid={home.treatment_header.isValid}
                placeholder={"Tedaviler Başlık"}
                required={true}
              />
            </div>
          </div>
        </div>
        <div class="flex flex-wrap my-4">
          <div class="w-full lg:w-3/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Yorum Spot
              </label>
              <Input
                bind:value={home.review_spot.value}
                bind:isValid={home.review_spot.isValid}
                placeholder={"Yorum Spot"}
                required={true}
              />
            </div>
          </div>
          <div class="w-full lg:w-9/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Yorum Başlık 
              </label>
              <Input
                bind:value={home.review_header.value}
                bind:isValid={home.review_header.isValid}
                placeholder={"Yorum Başlık "}
                required={true}
              />
            </div>
          </div>
        </div>
        <div class="flex flex-wrap my-4">
          <div class="w-full lg:w-3/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Harita Spot
              </label>
              <Input
                bind:value={home.map_spot.value}
                bind:isValid={home.map_spot.isValid}
                placeholder={"Harita Spot"}
                required={true}
              />
            </div>
          </div>
          <div class="w-full lg:w-9/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
              Harita Başlık 
              </label>
              <Input
                bind:value={home.map_header.value}
                bind:isValid={home.map_header.isValid}
                placeholder={"Harita Başlık "}
                required={true}
              />
            </div>
          </div>
        </div>
        <div class="flex flex-wrap my-4">
          <div class="w-full lg:w-3/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Harita Kutu Başlık
              </label>
              <Input
                bind:value={home.map_box_header.value}
                bind:isValid={home.map_box_header.isValid}
                placeholder={"Harita Kutu Başlık"}
                required={true}
              />
            </div>
          </div>
          <div class="w-full lg:w-9/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
              Harita Kutu Text 
              </label>
              <Input
                bind:value={home.map_box_desc.value}
                bind:isValid={home.map_box_desc.isValid}
                placeholder={"Harita Kutu Text  "}
                required={true}
              />
            </div>
          </div>
        </div>
        <div class="flex flex-wrap">
          <div class="w-full lg:w-12/12 px-4 text-right mt-2">
            <button
              on:click={addHome}
              disabled={!home.lang.isValid || home.lang.value==null}
              class="bg-blue-600 disabled:bg-red-300 text-white active:bg-bred-400 font-bold  text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 "
              type="button"
            >
              {$Translate("Save")}
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
