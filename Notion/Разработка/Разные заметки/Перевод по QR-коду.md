# Тинькофф
ru.tcsbank.mb.ui.deeplink.DeepLinkingActivity → ru.tcsbank.mb.ui.deeplink.AuthorizedDeepLinkingActivity
Коды действий здесь:
j20.l. Отсюда ссылаются на Enum с url действий.
```Java
package j20;
import j20.e;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;
import ru.tinkoff.commonchat.domain.message.content.MessageContent;
import ru.tinkoff.core.smartfields.api.preq.PreqFormInflater;
public enum f {
    ACCOUNT("/Account", (int) new j[]{j.b("accountId")}),
    ACCOUNT_ADDITIONAL_DETAILS("/AccountAdditionalDetails", (int) new j[]{j.b("accountId")}),
    ACCOUNT_INVEST_BOX("/Account/InvestBox"),
    ACCOUNT_REQUISITES("/AccountRequisites", (int) new j[]{j.b("accountId")}),
    ACTIVATE_CASH_LOAN("/ActivateCashLoan", (int) new j[]{j.b("accountId")}),
    ADD_TO_CALENDAR("/AddToCalendar", (int) new j[]{j.b("date"), j.a("eventName"), j.a("eventDescription"), j.a("allDayEvent"), j.a("recurrenceFrequency"), j.a("showEventScreen"), j.a("recurrenceEndDate"), j.a("notificationOffset")}),
    APP_IN_APP("/AppInApp"),
    APP_IN_APP_CART("/AppInApp/Cart"),
    ATMS("/ATMs", (int) new j[]{j.b("type"), j.a("currencies")}),
    ATTACH_CARD("/AttachCard"),
    BILLS_TO_PAY("/BillsToPay", (int) new j[]{j.a("providerId"), j.a("subscriptionId"), j.a("billId")}),
    BLOCK_CARD("/BlockCard", (int) new j[]{j.b("accountId"), j.b("ucid")}),
    BONUSES("/Bonuses"),
    C2C("/Pay/C2C"),
    CARD_LIMITS("/CardLimits"),
    CARD_PINS("/CardPins"),
    CARD_SERVICE("/CardServices", (int) new j[]{j.b("ucid"), j.b("accountId")}),
    CL_CHOOSE_TERMS("/ClChooseTerms", (int) new j[]{j.b("applicationIntegrationId")}),
    CHAT("/Chat", (int) new j[]{j.a("textParams"), j.a("conversationId")}),
    CINEMA_LIST("/CinemasList"),
    CINEMA_SCHEME("/CinemaTickets/Scheme", (int) new j[]{j.b("slotId"), j.b("movieId"), j.b("cinemaId"), j.b("date")}),
    CINEMA_TICKETS("/CinemaTickets"),
    CINEMA_TICKETS_CINEMAS("/CinemaTickets/Cinemas", (int) new j[]{j.a("cinemaId")}),
    CINEMA_TICKETS_MAP("/CinemaTickets/Map"),
    CINEMA_TICKETS_MOVIES("/CinemaTickets/Movies", (int) new j[]{j.a("movieId")}),
    CINEMA_TICKETS_MOVIES_SOON("/CinemaTickets/MoviesSoon"),
    CINEMA_TICKETS_MOVIES_TODAY("/CinemaTickets/MoviesToday"),
    CINEMA_TICKETS_MOVIE_SCHEDULE("/CinemaTickets/MovieSchedule", (int) new j[]{j.b("movieId"), j.a("city")}),
    CINEMA_TICKETS_SCHEDULE("/CinemaTickets/Schedule", (int) new j[]{j.a("movieId"), j.a("cinemaId")}),
    CONTACTS("/Contacts"),
    CURRENCY_RATES("/CurrencyRates"),
    DEPOSIT_ACCOUNT("/DepositAccount", (int) new j[]{j.b("accountId")}),
    DEPOSITION_POINTS("/DepositionPoints", (int) new j[]{j.a("partners")}),
    DEPOSIT_FULL_WITHDRAWAL("/DepositFullWithdrawal", (int) new j[]{j.b("depositId")}),
    ENTRY_SETTINGS("/EntrySettings"),
    INVOICE("/EInvoicing", (int) new j[]{j.b("providerId"), j.a("billId")}),
    KIDS_TASK_LIST("/KidsTasks", (int) new j[]{j.a("childId")}),
    LOYALTY_POINTS("/LoyaltyPoints", (int) new j[]{j.b("accountId")}),
    MAKE_APPOINTMENT("/MakeAppointment", (int) new j[]{j.b("tasksId")}),
    MALLS("/Malls"),
    MALLS_COLLECTIONS("/MallsCollections", (int) new j[]{j.b("city"), j.b("collectionCode")}),
    MALL_DETAILS("/Malls/MallDetails", (int) new j[]{j.b("mallId")}),
    MALL_SALE("/MallSale", (int) new j[]{j.b("saleId")}),
    MALL_SHOP_LIST("/Malls/ObjectsList", (int) new j[]{j.b("mallId"), j.b("shopType"), j.a("category"), j.a("saleId")}),
    MALL_SHOP_DETAILS("/Malls/ObjectDetails", (int) new j[]{j.b("objectId"), j.a("offerId")}),
    MEETING_DETAILS("/MeetingDetails", (int) new j[]{j.b("appointmentId")}),
    MENU_INFO("/MenuInfo"),
    MORE("/More"),
    MOVIE_COLLECTIONS("/MovieCollections", (int) new j[]{j.b("city"), j.b("collectionCode")}),
    OFFER("/Offer", (int) new j[]{j.b("offerType"), j.a("requireLoyalty"), j.a("newProductAccount")}),
    ORDERS_APP_IN_APP("/Orders/AppInApp"),
    ORDERS_CINEMA("/Orders/Cinema", (int) new j[]{j.b("orderId")}),
    ORDERS_CONCERT("/Orders/Concerts", (int) new j[]{j.b("orderId")}),
    ORDERS_LIST("/Orders"),
    ORDERS_RESTAURANT("/Orders/Restaurants", (int) new j[]{j.b("orderId")}),
    ORDERS_SPECTACLE("/Orders/Spectacles", (int) new j[]{j.b("orderId")}),
    ORDERS_BEAUTY("/Orders/BeautySalon", (int) new j[]{j.b("orderId")}),
    PAY("/Pay", (int) new j[]{j.a("ProviderGroup"), j.a("Provider")}),
    PAY_BY_ACCOUNT_ID("/PayByAccountID"),
    PAY_TEMPLATE("/Pay/Template", (int) new j[]{j.b("templateId")}),
    PAY_BY_MOBILE_NUMBER("/PayByMobileNumber"),
    PAYMENT_SCHEDULE("/Payment_schedule", (int) new j[]{j.b("accountId")}),
    PROLONGATION("/Prolongation", (int) new j[]{j.b("depositId")}),
    PUSH_STORY("/ShowStory"),
    REFILL_ACCOUNT_FROM_CARD("/Pay/RefillAccountFromCard", (int) new j[]{j.b("accountId")}),
    REPLENISH_KUPI_V_KREDIT("/ReplenishKupiVKredit", (int) new j[]{j.b("accountId")}),
    RESTAURANT_COLLECTIONS("/RestaurantCollections", (int) new j[]{j.b("city"), j.b("collectionCode")}),
    RESTAURANTS("/Restaurants", (int) new j[]{j.a("restaurantId")}),
    RESTAURANTS_FAVORITE("/Restaurants/Favorite"),
    RESTAURANTS_POLL("/Restaurants/Poll", (int) new j[]{j.a("city")}),
    SPECIAL_OFFERS("/SpecialOffers", (int) new j[]{j.a("offerId"), j.a("categoryCode"), j.a("mallId")}),
    SPORT("/Sport", (int) new j[]{j.b(MessageContent.SOURCE_FIELD)}),
    SPORT_LIST("/SportList", (int) new j[]{j.b("city")}),
    SPORT_NEXT_WEEKEND_LIST("/SportNextWeekendList", (int) new j[]{j.b("city")}),
    SPORT_COLLECTIONS("/SportCollections", (int) new j[]{j.b("city"), j.b("collectionCode")}),
    SPORT_TEAM_LIST("/SportTeamList", (int) new j[]{j.b("city"), j.b("teamId")}),
    SPORT_TICKETS("/SportTickets", (int) new j[]{j.a("eventId")}),
    SPORT_HALL_SCHEME("/SportHallScheme", (int) new j[]{j.b("eventId"), j.b("objectId"), j.b("hallId"), j.b("slotId")}),
    SPORT_SECTOR_SCHEME("/SportSectorScheme", (int) new j[]{j.b("eventId"), j.b("objectId"), j.b("hallId"), j.b("slotId"), j.b("sectorId")}),
    SPORT_ORDER("/Orders/Sport", (int) new j[]{j.b("orderId")}),
    SUBSCRIPTION_CREATE("/Subscriptions/Create", (int) new j[]{j.a("providerId")}),
    SUBSCRIPTION_DETAILS("/Subscriptions/Details", (int) new j[]{j.b("subscriptionId")}),
    TARIFF("/Tariff", (int) new j[]{j.a("accountId")}),
    TARIFF_LIMITS("/TariffLimits", (int) new j[]{j.b("accountId")}),
    TRANSFER_TO_PEOPLE("/TransferToPeople", (int) new j[]{j.a("targetAccountId")}),
    TRIPS("/Trips"),
    OPERATION_DETAILS("/Operation", (int) new j[]{j.b("id"), j.b("operationTime"), j.a("ucid")}),
    ACCOUNT_DOCUMENTS("/AccountDocuments"),
    ACTIVATE_CARD("/ActivateCard", (int) new j[]{j.b("ucid")}),
    ADD_DOCUMENT("/AddDocument"),
    ADDRESS("/Address"),
    BRING_FRIEND("/BringAFriend"),
    BRING_FRIEND_CONTACTS("/BringAFriend/Contacts"),
    BRING_FRIEND_INVITATIONS("/BringAFriend/Invitations"),
    BRING_FRIEND_PRODUCTS("/BringAFriend/Products", (int) new j[]{j.a("product")}),
    BROKER_ACCOUNT_APPLICATION("/BrokerAccountApplication"),
    CAR_LOAN_ADD_AUTO("/CarLoanAddAuto", (int) new j[]{j.b("accountId")}),
    CARD_ALL("/AllCard"),
    CARD_CREATE("/Cards/CreateApplication", (int) new j[]{j.b("programId"), j.a("XsellStrategyId")}),
    CARD_REQUISITES("/CardRequisites", (int) new j[]{j.b("ucid"), j.b("accountId")}),
    CASH_LOAN_APPLICATION("/CashLoanApplication", (int) new j[]{j.a("XsellStrategyId")}),
    COLLECT_MONEY_CREATE("/CM/Create"),
    CONCERTS_COLLECTIONS("/ConcertsCollections", (int) new j[]{j.b("city"), j.b("collectionCode")}),
    CONCERTS_GENRE_LIST("/ConcertsGenreList", (int) new j[]{j.b("city"), j.b("genre")}),
    CONCERTS_HALL_SCHEME("/ConcertsHallScheme", (int) new j[]{j.b("eventId"), j.b("objectId"), j.b("hallId"), j.b("slotId")}),
    CONCERTS_LIST("/ConcertsList", (int) new j[]{j.b("city")}),
    CONCERTS_NEXT_WEEKEND_LIST("/ConcertsNextWeekendList", (int) new j[]{j.b("city")}),
    CONCERTS_SECTOR_SCHEME("/ConcertsSectorScheme", (int) new j[]{j.b("eventId"), j.b("objectId"), j.b("hallId"), j.b("slotId"), j.b("sectorId")}),
    CONCERTS_TICKETS("/ConcertsTickets", (int) new j[]{j.a("eventId"), j.a("objectId")}),
    CONCERT_HALLS_LIST("/ConcerthallsList", (int) new j[]{j.b("city")}),
    CREATE_AUTOPAYMENT("/CreateAutopayment", (int) new j[]{j.a("templateId"), j.a("phone")}),
    DEPOSIT("/Deposit"),
    DETAIL_COLLECT_MONEY("/CM", (int) new j[]{j.a("invoiceId"), j.b("groupId")}),
    DOCUMENT_LIST("/DocumentsList"),
    ENTERTAINMENT("/Entertainment"),
    ESIA_REGISTRATION("/EsiaRegistration"),
    HIGH_CASHBACK("/HighCashBack", (int) new j[]{j.a("offerId")}),
    IIS_APPLICATION("/IisApplication"),
    INSURANCE_TRAVEL("/TravelInsurance"),
    INVEST_ADVISOR("/InvAdvisor"),
    INVESTMONEYBOX_AUTODEPOSIT_PARAMETERS("/InvestmoneyboxAutodepositParameters"),
    INVESTMONEYBOX_AUTODEPOSIT_SETTINGS("/InvestmoneyboxAutodepositSettings"),
    INVESTMONEYBOX_ONBOARDING_OPENING("/InvestmoneyboxOnboardingOpening"),
    INVESTMONEYBOX_ONBOARDING_ROUNDING("/InvestmoneyboxOnboardingRounding"),
    INTERFACE_SETTIGS("/InterfaceSettings"),
    INVITE_FRIEND("/InviteFriend"),
    ISSUE_ADDITIONAL_CARD("/IssueAdditionalCard", (int) new j[]{j.b("accountId")}),
    KIDS_TRACKING("/KidsTracking", (int) new j[]{j.a("portalId")}),
    LIST_PRODUCTS("/ListProducts"),
    MOBILE("/OrderTinkoffMobile"),
    NEW_PRODUCTS("/NewProducts", (int) new j[]{j.b("programId"), j.a("XsellStrategyId")}),
    NEW_RKO("/NewRKO", (int) new j[]{j.a("inn"), j.a("name")}),
    NEW_TINKOFF_JUNIOR("/NewTinkoffJunior"),
    ONBOARDING_SBP("/OnboardingSbp"),
    ONBOARDING_VISA("/OnboardingVisa"),
    PAY_FINES("/Pay/Fines"),
    PAY_SCAN_QR("/Pay/ScanQR"),
    PREMIUM_SERVICES("/PremiumServices"),
    PREPAID_CARD_LIMITS("/PrepaidCardLimitations", (int) new j[]{j.b("accountId")}),
    QR_CASH("/QrCash", (int) new j[]{j.a("amount")}),
    REGISTRATION("/Registration"),
    REISSUE("/Reissue", (int) new j[]{j.b("ucid")}),
    SIGN_UP("/SignUp", (int) new j[]{j.b("token")}),
    SPECTACLES_COLLECTIONS("/SpectaclesCollections", (int) new j[]{j.b("city"), j.b("collectionCode")}),
    SPECTACLES_GENRE_LIST("/SpectaclesGenreList", (int) new j[]{j.b("city"), j.b("genre")}),
    SPECTACLES_LIST("/SpectaclesList", (int) new j[]{j.b("city")}),
    TARGET("/Target"),
    TBUNDLE_DEPENDENT_ACTIVATION("/TbundlePartnerConnection", (int) new j[]{j.b("bundleCode"), j.b("dependentCode")}),
    TBUNDLE_MAIN_ACTIVATION("/TbundleCoreConnection", (int) new j[]{j.b("bundleCode")}),
    TBUNDLE_MAIN_OPTIONS("/TbundleMainOptions", (int) new j[]{j.b("bundleCode")}),
    TBUNDLE_DETAILS("/TbundleDetails", (int) new j[]{j.b("bundleCode")}),
    THEATRES_LIST("/TheatresList", (int) new j[]{j.b("city")}),
    THEATRES_TICKETS("/TheatresTickets", (int) new j[]{j.a("eventId"), j.a("objectId")}),
    THEATRES_SECTOR_SCHEME("/TheatresSectorScheme", (int) new j[]{j.b("eventId"), j.b("objectId"), j.b("hallId"), j.b("slotId"), j.b("sectorId")}),
    THEATRES_HALL_SCHEME("/TheatresHallScheme", (int) new j[]{j.b("eventId"), j.b("objectId"), j.b("slotId"), j.b("hallId")}),
    TRANCHES_OFFER("/TranchesOffers", (int) new j[]{j.a("categoryCode")}),
    TRAVELS("/Travels"),
    TRAVELS_HOTELS("/TravelsHotels", (int) new j[]{j.b("label")}),
    TRAVELS_ORDERS_FLIGHTS("/Orders/Flights", (int) new j[]{j.b("orderId"), j.b(MessageContent.SOURCE_FIELD)}),
    TRAVELS_ORDERS_HOTELS("/Orders/Hotels", (int) new j[]{j.b("reservationId"), j.b(MessageContent.SOURCE_FIELD)}),
    TRAVELS_WEB("/TravelsWeb", (int) new j[]{j.b("id")}),
    TRAVELS_WEB_FLIGHT("/TravelsWebFlight", (int) new j[]{j.b(PreqFormInflater.J_KEY_LINK)}),
    USER_REQUESTS("/UserRequests"),
    USERS_CONTACTS("/UsersContacts", (int) new j[]{j.b("contactId")}),
    WALLET("/Wallet"),
    ZERO_LIABILITY("/AddZeroLiability"),
    CREATE_KIDS_SHARED_SAVING("/CreateKidsSharedSaving"),
    ACCOUNT_REFILL(e.b.f5780a, d.WWW_TINKOFF_RU, "/rm/*/*"),
    APP_PERMISSIONS(e.b.f5780a, d.WWW_TINKOFF_RU, "/ta/*/*"),
    SBP_QR(e.b.f5780a, d.QR_NSPK_RU, "/*");
    
    public final List<j> deeplinkParams;
    public final d host;
    public final String path;
    public final e scheme;
    /* access modifiers changed from: public */
    f(e eVar, d dVar, String str, List<j> list) {
        this.scheme = eVar;
        this.host = dVar;
        this.path = str;
        this.deeplinkParams = list;
    }
    public static f findByOrdinal(int i) {
        for (f fVar : values()) {
            if (fVar.ordinal() == i) {
                return fVar;
            }
        }
        return null;
    }
    public List<j> getDeeplinkParams() {
        return this.deeplinkParams;
    }
    public d getHost() {
        return this.host;
    }
    public String getPath() {
        return this.path;
    }
    public e getScheme() {
        return this.scheme;
    }
    /* access modifiers changed from: public */
    f(e eVar, d dVar, String str) {
        this(r8, r9, eVar, dVar, str, Collections.emptyList());
    }
    /* access modifiers changed from: public */
    f(String str, List<j> list) {
        this(r8, r9, e.a.f5779a, d.MAIN, str, list);
    }
    /* access modifiers changed from: public */
    f(String str) {
        this(r2, r3, str, (List<j>) Collections.emptyList());
    }
    /* access modifiers changed from: public */
    f(String str, j... jVarArr) {
        this(r1, r2, str, (List<j>) Arrays.asList(jVarArr));
    }
}
```
## Как генерировать QR-код
На сайте тинькова пример кода: [https://help.tinkoff.ru/currency-ruble/replenish/qr-code](https://help.tinkoff.ru/currency-ruble/replenish/qr-code/)
```Java
ST00012|Name=?????????????? ??????????????? ???????? ???? ????????????|PersonalAcc=40802810500000206666|BankName=?? "???????? ????"|BIC=044525974|CorrespAcc=30101810145250000974|PayeeINN=502604714510|KPP=0
```
Пример на Хабре:

> [!info] Как создать QR код для оплаты в платежной системе  
> Сегодня, хочу рассказать, реальную истории из жизни.  
> [https://habr.com/ru/post/450978/](https://habr.com/ru/post/450978/)  

> [!info] ГОСТ для создания QR-кода платежа  
> Подробности Категория: Полезные программы, справочники, обучение Чтобы сформировать QR-код для оплаты квитаниции используем следующий стандарт.  
> [https://jdevelop.info/articles/programs-tutorials/558-gost-dlya-sozdaniya-qr-koda-platezha](https://jdevelop.info/articles/programs-tutorials/558-gost-dlya-sozdaniya-qr-koda-platezha)  
Успешный перевод с Тинькофф на Сбер

> [!info] Сбербанк Онлайн  
>  
> [https://node2.online.sberbank.ru/PhizIC/private/payments/view.do?id=30225676786&history=true&archive=false&creationType=8](https://node2.online.sberbank.ru/PhizIC/private/payments/view.do?id=30225676786&history=true&archive=false&creationType=8)