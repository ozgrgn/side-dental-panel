<script>
  import FooterAdmin from "$components/Footers/FooterAdmin.svelte";
  import { Route, Router } from "svelte-navigator";
  import AdminNavbar from "./Navbar.svelte";

  import Dashboard from "./Dashboard.svelte";

  import CreateSlider from "./slider/CreateSlider.svelte";
  import Sliders from "./slider/Sliders.svelte";
  import UpdateSlider from "./slider/UpdateSlider.svelte";

  import UpdateAdmin from "./admin/UpdateAdmin.svelte";
  import CreateAdmin from "./admin/CreateAdmin.svelte";
  import Admins from "./admin/Admins.svelte";
  import UpdateLang from "./lang/UpdateLang.svelte";
  import CreateLang from "./lang/CreateLang.svelte";
  import Langs from "./lang/Langs.svelte";
  import UpdateHome from "./homePage/UpdateHome.svelte";
  import CreateHome from "./homePage/CreateHome.svelte";
  import Homes from "./homePage/Homes.svelte";
  import UpdateAbout from "./about/UpdateAbout.svelte";
  import CreateAbout from "./about/CreateAbout.svelte";
  import Abouts from "./about/Abouts.svelte";
  import UpdateTreatment from "./treatment/UpdateTreatment.svelte";
  import CreateTreatment from "./treatment/CreateTreatment.svelte";
  import Treatments from "./treatment/Treatments.svelte";
  import UpdateTreatmentPage from "./treatmentPage/UpdateTreatmentPage.svelte";
  import CreateTreatmentPage from "./treatmentPage/CreateTreatmentPage.svelte";
  import TreatmentPages from "./treatmentPage/TreatmentPages.svelte";
  import UpdateContact from "./contact/UpdateContact.svelte";
  import CreateContact from "./contact/CreateContact.svelte";
  import Contacts from "./contact/Contacts.svelte";
  import UpdateGeneral from "./general/UpdateGeneral.svelte";
  import CreateGeneral from "./general/CreateGeneral.svelte";
  import Generals from "./general/Generals.svelte";
  import UpdateTranslate from "./translate/UpdateTranslate.svelte";
  import CreateTranslate from "./translate/CreateTranslate.svelte";
  import Translates from "./translate/Translates.svelte";
  import { modal } from "../../services/store";
  import Modal from "svelte-simple-modal";
  import CreateFeatures from "./features/CreateFeatures.svelte";
  import Features from "./features/Features.svelte";
  import UpdateFeatures from "./features/UpdateFeatures.svelte";
  import UpdateGroup from "./group/UpdateGroup.svelte";
  import CreateGroup from "./group/CreateGroup.svelte";
  import Groups from "./group/Groups.svelte";
  import UpdateFaq from "./faq/UpdateFaq.svelte";
  import CreateFaq from "./faq/CreateFaq.svelte";
  import Faqs from "./faq/Faqs.svelte";
  import UpdateReview from "./reviews/UpdateReview.svelte";
  import CreateReview from "./reviews/CreateReview.svelte";
  import Reviews from "./reviews/Reviews.svelte";
  // let userAuthSubscription = user.subscribe(async (auth) => {
  //   if (!auth) {
  //     navigate("/auth/login");
  //     SOCKET.stopConnection();
  //     if (window.location.pathname.indexOf("admin") != -1) {
  //       navigate("/auth/login");
  //     }
  //   } else {
  //     let response = await RestService.verifyToken();
  //     if (response && response.status) {
  //       SOCKET.startConnection();
  //       if (
  //         window.location.pathname == "/auth/login" ||
  //         window.location.pathname == "/panel" ||

  //         window.location.pathname == "/panel/"
  //       ) {
  //         navigate("/panel/dashboard");
  //       }
  //     } else {
  //       user.set(null);
  //     }
  //   }
  // });
  // onDestroy(() => {
  //   userAuthSubscription;
  // });
</script>

<Modal show={$modal} />
<div>
  <!-- <Sidebar /> -->

  <div class="relative bg-blueGray-100">
    <AdminNavbar />

    <div class="relative bg-blue-600 md:pt-32 pb-32 pt-12" />

    <div class="px-2 mx-auto w-full -m-24">
      <Router>
        <!-- Dashboard -->
        <Route path="dashboard" component={Dashboard} />

        <!-- Admin -->
        <Route path="update-admin/:adminId" component={UpdateAdmin} />

        <Route path="create-admin" component={CreateAdmin} />

        <Route path="admins" component={Admins} />

        <!-- Slider -->
        <Route path="update-slider/:sliderId" component={UpdateSlider} />

        <Route path="create-slider" component={CreateSlider} />

        <Route path="sliders" component={Sliders} />

        <!-- Ana Sayfa -->
        <Route path="update-home/:homeId" component={UpdateHome} />

        <Route path="create-home" component={CreateHome} />

        <Route path="homes" component={Homes} />

        <!-- Özellikler -->
        <Route path="update-feature/:featureId" component={UpdateFeatures} />

        <Route path="create-feature" component={CreateFeatures} />

        <Route path="features" component={Features} />

        <!-- Hakkımızda -->
        <Route path="update-about/:aboutId" component={UpdateAbout} />

        <Route path="create-about" component={CreateAbout} />

        <Route path="abouts" component={Abouts} />

        <!-- Tedavi-Sayfası -->
        <Route
          path="update-treatmentpage/:treatments_pageId"
          component={UpdateTreatmentPage}
        />

        <Route path="create-treatmentpage" component={CreateTreatmentPage} />

        <Route path="treatmentpages" component={TreatmentPages} />
        <!-- İletişim -->
        <Route path="update-contact/:contactId" component={UpdateContact} />

        <Route path="create-contact" component={CreateContact} />

        <Route path="contacts" component={Contacts} />
        <!-- Genel Bilgiler -->
        <Route path="update-general/:generalId" component={UpdateGeneral} />

        <Route path="create-general" component={CreateGeneral} />

        <Route path="generals" component={Generals} />
        <!-- Çeviriler -->
        <Route
          path="update-translate/:translateId"
          component={UpdateTranslate}
        />

        <Route path="create-translate" component={CreateTranslate} />

        <Route path="translates" component={Translates} />
        <!-- Diller -->
        <Route path="update-lang/:langId" component={UpdateLang} />

        <Route path="create-lang" component={CreateLang} />

        <Route path="langs" component={Langs} />

        <!-- Tedaviler -->
        <Route
          path="update-treatment/:treatmentId"
          component={UpdateTreatment}
        />

        <Route path="create-treatment" component={CreateTreatment} />

        <Route path="treatments" component={Treatments} />
        <!-- Groups -->
        <Route path="update-group/:groupId" component={UpdateGroup} />

        <Route path="create-group" component={CreateGroup} />

        <Route path="groups" component={Groups} />
           <!-- Faqs -->
           <Route path="update-faq/:faqId" component={UpdateFaq} />

           <Route path="create-faq" component={CreateFaq} />
   
           <Route path="faqs" component={Faqs} />
                <!-- Reviews -->
                <Route path="update-review/:reviewId" component={UpdateReview} />

                <Route path="create-review" component={CreateReview} />
        
                <Route path="reviews" component={Reviews} />
      </Router>

      <FooterAdmin />
    </div>
  </div>
</div>
