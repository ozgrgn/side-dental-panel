<script>
  import Alert from "$components/Alert.svelte";
  import ImageArray from "$components/Form/ImageArray.svelte";
  import Input from "$components/Form/Input.svelte";
  import NumberInput from "$components/Form/NumberInput.svelte";
  import Select from "$components/Form/Select.svelte";
  import Textarea from "$components/Form/Textarea.svelte";
  import TextEditor from "$components/Form/TextEditor.svelte";
  import Switch from "$components/Switch.svelte";
  import { Translate, TranslateApiMessage } from "$services/language";
  import RestService from "$services/rest.js";
  import ToastService from "$services/toast";
  import { navigate, useParams } from "svelte-navigator";
  import { bind } from "svelte-simple-modal";
  const deleteTreatmentApprove = (treatmentId) => {
    modal.set(
      bind(Alert, {
        message: "Bu işlemi onaylıyor musunuz ?",
        answer: (message) => {
          if (message) {
            deleteTreatment(treatmentId);
          }
          modal.set(null);
        },
      })
    );
  };

  const params = useParams();

  let deleteImage = (index) => {
    treatment.images.splice(index, 1);
    treatment.images = treatment.images;
  };

  let treatment;
  let langs = [];

  let values = [
    { key: "lang", customValue: null },
    { key: "title", customValue: null },
    { key: "perma", customValue: null },
    { key: "spot", customValue: null },
    { key: "header", customValue: null },
    { key: "shortDesc", customValue: null },
    { key: "text", customValue: null },
    { key: "hp", customValue: null },
    { key: "icon", customValue: null },
    { key: "order", customValue: null },
    { key: "isActive", customValue: null },
  ];
  const getLang = async () => {
    let response = await RestService.getLangs(undefined, undefined);
    langs = response["langs"];
    console.log(langs, "langs");
  };
  getLang();
  const updateTreatment = async () => {
    let editedTreatment = {};
    editedTreatment.images = treatment.images;
    editedTreatment.logos = treatment.logos;
    values.map((v) => {
      editedTreatment[v.key] = treatment[v.key].value;
    });

    let response = await RestService.updateTreatment(treatment._id, editedTreatment);
    if (response["status"]) {
      ToastService.success($Translate("Successfully-completed"));
      navigate("/panel/treatments");
    } else {
      ToastService.error($TranslateApiMessage(response.message));
    }
  };

  const getTreatment = async () => {
    let response = await RestService.getTreatment($params.treatmentId);

    if (response["status"]) {
      values.map((v) => {
        if (v.customValue) {
          response["treatment"][v.key] = {
            value: response["treatment"][v.key][v.customValue],
          };
        } else {
          response["treatment"][v.key] = { value: response["treatment"][v.key] };
        }
      });
      treatment = {
        ...response["treatment"],
      };
    } else {
      ToastService.error($TranslateApiMessage(response.message));
    }
  };

  getTreatment();

  const deleteTreatment = async (treatmentId) => {
    let response = await RestService.deleteTreatment(treatmentId);
    if (response["status"]) {
      ToastService.success("İşlem başarılı");
      navigate("/panel/treatments");
    } else {
      ToastService.success("İşlem başarılı");
    }
  };
</script>

<div class="flex flex-wrap mt-4 h-screen relative">
  <div class="w-full mb-12 px-2 lg:px-4 ">
    <div class="flex justify-between">
      <button
        class="bg-white text-blue-600 hover:text-red-700 mb-2 border rounded font-bold text-xs px-4 py-2 rounded shadow hover:shadow-lg outline-none focus:outline-none mr-1 "
        type="button"
        on:click={() => {
          navigate("/panel/treatments");
        }}
      >
        <i class="fa fa-arrow-left" />
        {$Translate("Back")}
      </button>

      <button
        class="bg-white text-blue-600 hover:text-red-700 mb-2 border rounded font-bold text-xs px-4 py-2 rounded shadow hover:shadow-lg outline-none focus:outline-none mr-1 "
        type="button"
        on:click={() => deleteTreatmentApprove($params.treatmentId)}
      >
        <i class="fa fa-trash" />
        Sil
      </button>
    </div>

    <div
      class="relative flex flex-col min-w-0 break-words w-full mb-6 shadow-lg rounded bg-gray-100"
    >
      <div class="rounded-t mb-0 px-4 py-3 border-0">
        <div class="text-center flex justify-between">
          <h3 class="font-semibold text-lg text-blueGray-700">
            Treatment güncelle
          </h3>
        </div>
      </div>
      <div class="flex-auto px-4 lg:px-10 py-10 pt-0">
        {#if treatment}
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
                bind:value={treatment.lang.value}
                bind:isValid={treatment.lang.isValid}
                values={langs}
                title={"Dil Seçin"}
                valuesKey={"lang"}
                valuesTitleKey={"title"}
                customClass={"w-full"}
              />
            </div>
          </div>

          <div class="w-full lg:w-3/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                İsim
              </label>
              <Input
                bind:value={treatment.title.value}
                bind:isValid={treatment.title.isValid}
                placeholder={"Tedavi İsmi"}
                required={true}
              />
            </div>
          </div>
          <div class="w-full lg:w-2/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Perma
              </label>

              <Input
              bind:value={treatment.perma.value}
              bind:isValid={treatment.perma.isValid}
              placeholder={"Tedavi Perma"}
              required={true}
            />
            </div>
          </div>
          <div class="w-full lg:w-2/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Sıra
              </label>

              <NumberInput
                bind:value={treatment.order.value}
                bind:isValid={treatment.order.isValid}
                placeholder={"Sıra"}
                required={true}
              />
            </div>
          </div>
          <div class="flex w-full justify-around lg:w-2/12 px-4">
            <div class="  mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="rectangleBanner"
              >
                Anasayfa ?
              </label>

              <Switch bind:value={treatment.hp.value} />
            </div>

            <div class="mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="rectangleBanner"
              >
                Aktif mi ?
              </label>

              <Switch bind:value={treatment.isActive.value} />
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
                Spot
              </label>
              <Input
                bind:value={treatment.spot.value}
                bind:isValid={treatment.spot.isValid}
                placeholder={"Tedavi Spot"}
                required={true}
              />
            </div>
          </div>
          <div class="w-full lg:w-3/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Başlık
              </label>
              <Input
                bind:value={treatment.header.value}
                bind:isValid={treatment.header.isValid}
                placeholder={"Tedavi Başlığı"}
                required={true}
              />
            </div>
          </div>
          <div class="w-full lg:w-6/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Kısa Açıklama
              </label>
              <Input
                bind:value={treatment.shortDesc.value}
                bind:isValid={treatment.shortDesc.isValid}
                placeholder={"Tedavi Başlık"}
                required={true}
              />
            </div>
          </div>

          <div class="w-full lg:w-6/12 px-4">
            <div class="relative w-full mb-3">
              <label
                class="block  text-blueGray-600 text-xs font-bold mb-2"
                for="grid-name"
              >
                Açıklama
              </label>

              <TextEditor
                placeholder={"Text 1"}
                bind:value={treatment.text.value}
                bind:incomingValue={treatment.text.value}

              />
            </div>
          </div>

          <div class="w-full md:flex lg:w-6/12 px-4 ">
            <div class="w-full lg:w-6/12">
              <div class="relative w-full mb-3">
                <label
                  class="block  text-blueGray-600 text-xs font-bold mb-2"
                  for="grid-name"
                >
                  Icon SVG
                </label>

                <Textarea
                  placeholder={" Icon SVG"}
                  bind:value={treatment.icon.value}
                />
              </div>
            </div>
            <div class="lg:w-6/12 w-full px-4 pt-4">
              <div class="">
                <div class=" ">
                  {#each treatment.images as Image, index}
                    <div class="border mt-2 p-1 grid grid-flow-col">
                      <span
                        class="px-2 flex flex-col justify-center text-blueGray-600 text-xs font-bold"
                        >{index + 1}.{"Resim"}</span
                      >
                      <div class="col-span-2">
                        <ImageArray bind:value={treatment.images[index].image} />
                      </div>
                      <div class="flex flex-col justify-center items-end">
                        <button
                          on:click={() => deleteImage(index)}
                          class="w-14 bg-red-500 hover:bg-red-600 text-white font-bold text-xs m-2 px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none"
                          type="button"
                        >
                          SİL
                        </button>
                      </div>
                    </div>
                  {/each}
                </div>
              </div>
              <button
                on:click={() => (treatment.images = [...treatment.images, { image: null }])}
                class=" mt-2 bg-red-400 disabled:bg-red-300 text-white active:bg-blue-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none ease-linear transition-all duration-150"
                type="button"
              >
                Tedavi Resmi Ekle
              </button>
            </div>
          </div>

        </div>
          <div class="flex flex-wrap">
            <div class="w-full lg:w-12/12 px-4 text-right mt-5">
              <button
                on:click={() => updateTreatment()}
                disabled={!treatment.lang.isValid }
                class="bg-blue-600 disabled:bg-red-300 text-white active:bg-bred-400 font-bold  text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 "
                type="button"
              >
                {$Translate("Update")}
              </button>
            </div>
          </div>
        {/if}
      </div>
    </div>
  </div>
</div>
