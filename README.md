//+------------------------------------------------------------------+
//|                                                     BoxIndicator.mq4 |
//|                        Modified by GPT                              |
//+------------------------------------------------------------------+
#property indicator_chart_window

// ورودی‌های عمومی

input int DaysBack = 0;
input string STOP = "خط استاپ";
input bool ShowLineStopLevel = FALSE;
input int LineStopLevel = 51;
input string BreakEven = "خط بریک ایون";
input bool ShowLinebreakEven = true;
input int LinebreakEven = 88;
input color BoxColorBreakEven = Yellow;
input string TPPOSITION = "تی پی";
input bool ShowTP = FALSE;
input int TP = 138;
input color BoxTP = Red;

// تنظیمات سشن‌ها
input string StartENDBOX = "ساعت شروع و پایان پیش سشن";
input string StartTimeAsia = "02:00";
input string EndTimeAsia = "02:59";
input string StartTimeOuro = "09:00";
input string EndTimeOuro = "09:59";
input string StartTimeUsa1 = "14:00";
input string EndTimeUsa1 = "14:59";
input string StartTimeUsa2 = "14:30";
input string EndTimeUsa2 = "15:29";

// تنظیمات هر سشن برای باکس‌های 1 ساعته و 4 ساعته آسیا
input  string Asia =" تنظیمات باکس آسیا";
input int DistanceFromTopfor1hoursAsia = 149;
input int DistanceFromBottomfor1hoursAsia = 149;
input int BoxThicknessfor1hoursAsia = 130;
input color BoxColor1hoursAsia = DeepSkyBlue;
input color MiddleBoxColor1hoursAsia = DodgerBlue;
input int DistanceFromTopfor4hoursAsia = 299;
input int DistanceFromBottomfor4hoursAsia = 299;
input int BoxThicknessfor4hoursAsia = 280;
input color BoxColor4hoursAsia = DeepSkyBlue;
input color MiddleBoxColor4hoursAsia = DodgerBlue;

// تنظیمات هر سشن برای باکس‌های 1 ساعته و 4 ساعته اروپا (Ouro)
input  string Uoro =" تنظیمات باکس اروپا";
input int DistanceFromTopfor1hoursOuro = 149;
input int DistanceFromBottomfor1hoursOuro = 149;
input int BoxThicknessfor1hoursOuro = 130;
input color BoxColor1hoursOuro = DarkGray;
input color MiddleBoxColor1hoursOuro = SlateGray;
input int DistanceFromTopfor4hoursOuro = 299;
input int DistanceFromBottomfor4hoursOuro = 299;
input int BoxThicknessfor4hoursOuro = 280;
input color BoxColor4hoursOuro = DarkGray;
input color MiddleBoxColor4hoursOuro = SlateGray;

// تنظیمات هر سشن برای باکس‌های 1 ساعته و 4 ساعته آمریکا 1
input  string Usa1 =" تنظیمات باکس امریکا 1 ";
input int DistanceFromTopfor1hoursUsa1 = 149;
input int DistanceFromBottomfor1hoursUsa1 = 149;
input int BoxThicknessfor1hoursUsa1 = 130;
input color BoxColor1hoursUsa1 = LimeGreen;
input color MiddleBoxColor1hoursUsa1 = LightSeaGreen;
input int DistanceFromTopfor4hoursUsa1 = 299;
input int DistanceFromBottomfor4hoursUsa1 = 299;
input int BoxThicknessfor4hoursUsa1 = 280;
input color BoxColor4hoursUsa1 = LimeGreen;
input color MiddleBoxColor4hoursUsa1 = LightSeaGreen;

// تنظیمات هر سشن برای باکس‌های 1 ساعته و 4 ساعته آمریکا 2
input  string Usa2 =" تنظیمات باکس امریکا 2 ";
input int DistanceFromTopfor1hoursUsa2 = 149;
input int DistanceFromBottomfor1hoursUsa2 = 149;
input int BoxThicknessfor1hoursUsa2 = 130;
input color BoxColor1hoursUsa2 = Tan;
input color MiddleBoxColor1hoursUsa2 = RosyBrown;
input int DistanceFromTopfor4hoursUsa2 = 299;
input int DistanceFromBottomfor4hoursUsa2 = 299;
input int BoxThicknessfor4hoursUsa2 = 280;
input color BoxColor4hoursUsa2 = Tan;
input color MiddleBoxColor4hoursUsa2 = RosyBrown;

// ورودی‌های مربوط به هر روز و هر باکس (برای تمامی هشت باکس)

// دوشنبه
input  string Monday ="دوشنبه" ;
input bool DisableMonday = false; // خاموش/روشن کردن دوشنبه
input  string MondayAsia = "یک ساعته و چهار ساعته آسیا"; 
input bool ShowMondayAsia1H_TopBox = true;
input bool ShowMondayAsia1H_BottomBox = true;
input bool ShowMondayAsia1H_MiddleUpBox = true;
input bool ShowMondayAsia1H_MiddleDownBox = true;
input bool ShowMondayAsia4H_TopBox = true;
input bool ShowMondayAsia4H_BottomBox = true;
input bool ShowMondayAsia4H_MiddleUpBox = true;
input bool ShowMondayAsia4H_MiddleDownBox = true;
input  string MondayOuro = "یک ساعته و چهار ساعته اروپا" ;
input bool ShowMondayOuro1H_TopBox = false;
input bool ShowMondayOuro1H_BottomBox = false;
input bool ShowMondayOuro1H_MiddleUpBox = true;
input bool ShowMondayOuro1H_MiddleDownBox = true;
input bool ShowMondayOuro4H_TopBox = true;
input bool ShowMondayOuro4H_BottomBox = true;
input bool ShowMondayOuro4H_MiddleUpBox = true;
input bool ShowMondayOuro4H_MiddleDownBox = true;
input string MondayUsa1 = "یک ساعته و چهار ساعته امریکا 1" ;
input bool ShowMondayUsa1_1H_TopBox = true;
input bool ShowMondayUsa1_1H_BottomBox = true;
input bool ShowMondayUsa1_1H_MiddleUpBox = false;
input bool ShowMondayUsa1_1H_MiddleDownBox = false;
input bool ShowMondayUsa1_4H_TopBox = false;
input bool ShowMondayUsa1_4H_BottomBox = false;
input bool ShowMondayUsa1_4H_MiddleUpBox = false;
input bool ShowMondayUsa1_4H_MiddleDownBox = false;
input string MondayUsa2 = "یک ساعته و چهار ساعته امریکا 2" ;
input bool ShowMondayUsa2_1H_TopBox = true;
input bool ShowMondayUsa2_1H_BottomBox = true;
input bool ShowMondayUsa2_1H_MiddleUpBox = true;
input bool ShowMondayUsa2_1H_MiddleDownBox = true;
input bool ShowMondayUsa2_4H_TopBox = false;
input bool ShowMondayUsa2_4H_BottomBox = false;
input bool ShowMondayUsa2_4H_MiddleUpBox = false;
input bool ShowMondayUsa2_4H_MiddleDownBox = false;

// سه‌شنبه
input  string Tuesday ="سشنبه" ;
input bool DisableTuesday = false; // خاموش/روشن کردن سه‌شنبه
input  string TuesdayAsia = "یک ساعته و چهار ساعته آسیا"; 
input bool ShowTuesdayAsia1H_TopBox = true;
input bool ShowTuesdayAsia1H_BottomBox = true;
input bool ShowTuesdayAsia1H_MiddleUpBox = true;
input bool ShowTuesdayAsia1H_MiddleDownBox = true;
input bool ShowTuesdayAsia4H_TopBox = true;
input bool ShowTuesdayAsia4H_BottomBox = true;
input bool ShowTuesdayAsia4H_MiddleUpBox = true;
input bool ShowTuesdayAsia4H_MiddleDownBox = true;
input  string TuesdayOuro = "یک ساعته و چهار ساعته اروپا" ;
input bool ShowTuesdayOuro1H_TopBox = false;
input bool ShowTuesdayOuro1H_BottomBox = false;
input bool ShowTuesdayOuro1H_MiddleUpBox = false;
input bool ShowTuesdayOuro1H_MiddleDownBox = false;
input bool ShowTuesdayOuro4H_TopBox = true;
input bool ShowTuesdayOuro4H_BottomBox = true;
input bool ShowTuesdayOuro4H_MiddleUpBox = true;
input bool ShowTuesdayOuro4H_MiddleDownBox = true;
input string TuesdayUsa1 = "یک ساعته و چهار ساعته امریکا 1" ;
input bool ShowTuesdayUsa1_1H_TopBox = false;
input bool ShowTuesdayUsa1_1H_BottomBox = false;
input bool ShowTuesdayUsa1_1H_MiddleUpBox = true;
input bool ShowTuesdayUsa1_1H_MiddleDownBox = true;
input bool ShowTuesdayUsa1_4H_TopBox = true;
input bool ShowTuesdayUsa1_4H_BottomBox = true;
input bool ShowTuesdayUsa1_4H_MiddleUpBox = true;
input bool ShowTuesdayUsa1_4H_MiddleDownBox = true;
input string TuesdayUsa2 = "یک ساعته و چهار ساعته امریکا 2" ;
input bool ShowTuesdayUsa2_1H_TopBox = false;
input bool ShowTuesdayUsa2_1H_BottomBox = false;
input bool ShowTuesdayUsa2_1H_MiddleUpBox = false;
input bool ShowTuesdayUsa2_1H_MiddleDownBox = false;
input bool ShowTuesdayUsa2_4H_TopBox = true;
input bool ShowTuesdayUsa2_4H_BottomBox = true;
input bool ShowTuesdayUsa2_4H_MiddleUpBox = false;
input bool ShowTuesdayUsa2_4H_MiddleDownBox = false;

// چهارشنبه
input  string Wednesday ="چهارشنبه" ;
input bool DisableWednesday = false; // خاموش/روشن کردن چهارشنبه
input string WednesdayAsia = "یک ساعته و چهار ساعته آسیا"; 
input bool ShowWednesdayAsia1H_TopBox = true;
input bool ShowWednesdayAsia1H_BottomBox = true;
input bool ShowWednesdayAsia1H_MiddleUpBox = true;
input bool ShowWednesdayAsia1H_MiddleDownBox = true;
input bool ShowWednesdayAsia4H_TopBox = true;
input bool ShowWednesdayAsia4H_BottomBox = true;
input bool ShowWednesdayAsia4H_MiddleUpBox = true;
input bool ShowWednesdayAsia4H_MiddleDownBox = true;
input  string WednesdayOuro = "یک ساعته و چهار ساعته اروپا" ;
input bool ShowWednesdayOuro1H_TopBox = true;
input bool ShowWednesdayOuro1H_BottomBox = true;
input bool ShowWednesdayOuro1H_MiddleUpBox = false;
input bool ShowWednesdayOuro1H_MiddleDownBox = false;
input bool ShowWednesdayOuro4H_TopBox = false;
input bool ShowWednesdayOuro4H_BottomBox = false;
input bool ShowWednesdayOuro4H_MiddleUpBox = true;
input bool ShowWednesdayOuro4H_MiddleDownBox = true;
input string WednesdayUsa1 = "یک ساعته و چهار ساعته امریکا 1" ;
input bool ShowWednesdayUsa1_1H_TopBox = false;
input bool ShowWednesdayUsa1_1H_BottomBox = false;
input bool ShowWednesdayUsa1_1H_MiddleUpBox = false;
input bool ShowWednesdayUsa1_1H_MiddleDownBox = false;
input bool ShowWednesdayUsa1_4H_TopBox = false;
input bool ShowWednesdayUsa1_4H_BottomBox = false;
input bool ShowWednesdayUsa1_4H_MiddleUpBox = false;
input bool ShowWednesdayUsa1_4H_MiddleDownBox = false;
input string WednesdayUsa2 = "یک ساعته و چهار ساعته امریکا 2" ;
input bool ShowWednesdayUsa2_1H_TopBox = false;
input bool ShowWednesdayUsa2_1H_BottomBox = false;
input bool ShowWednesdayUsa2_1H_MiddleUpBox = false;
input bool ShowWednesdayUsa2_1H_MiddleDownBox = false;
input bool ShowWednesdayUsa2_4H_TopBox = true;
input bool ShowWednesdayUsa2_4H_BottomBox = true;
input bool ShowWednesdayUsa2_4H_MiddleUpBox = false;
input bool ShowWednesdayUsa2_4H_MiddleDownBox = false;

// پنج شنبه
input  string Thursday ="پنج شنبه" ;
input bool DisableThursday = false; // خاموش/روشن کردن پنج‌شنبه
input string ThursdayAsia = "یک ساعته و چهار ساعته آسیا"; 
input bool ShowThursdayAsia1H_TopBox = true;
input bool ShowThursdayAsia1H_BottomBox = true;
input bool ShowThursdayAsia1H_MiddleUpBox = true;
input bool ShowThursdayAsia1H_MiddleDownBox = true;
input bool ShowThursdayAsia4H_TopBox = false;
input bool ShowThursdayAsia4H_BottomBox = false;
input bool ShowThursdayAsia4H_MiddleUpBox = false;
input bool ShowThursdayAsia4H_MiddleDownBox = false;
input  string ThursdayOuro = "یک ساعته و چهار ساعته اروپا" ;
input bool ShowThursdayOuro1H_TopBox = true;
input bool ShowThursdayOuro1H_BottomBox = true;
input bool ShowThursdayOuro1H_MiddleUpBox = true;
input bool ShowThursdayOuro1H_MiddleDownBox = true;
input bool ShowThursdayOuro4H_TopBox =false ;
input bool ShowThursdayOuro4H_BottomBox = false;
input bool ShowThursdayOuro4H_MiddleUpBox = false;
input bool ShowThursdayOuro4H_MiddleDownBox = false;
input string ThursdayUsa1 = "یک ساعته و چهار ساعته امریکا 1" ;
input bool ShowThursdayUsa1_1H_TopBox = false;
input bool ShowThursdayUsa1_1H_BottomBox = false;
input bool ShowThursdayUsa1_1H_MiddleUpBox = false;
input bool ShowThursdayUsa1_1H_MiddleDownBox = false;
input bool ShowThursdayUsa1_4H_TopBox = false;
input bool ShowThursdayUsa1_4H_BottomBox = false;
input bool ShowThursdayUsa1_4H_MiddleUpBox = true;
input bool ShowThursdayUsa1_4H_MiddleDownBox = true;
input string ThursdayUsa2 = "یک ساعته و چهار ساعته امریکا 2" ;
input bool ShowThursdayUsa2_1H_TopBox = false;
input bool ShowThursdayUsa2_1H_BottomBox = false;
input bool ShowThursdayUsa2_1H_MiddleUpBox = false;
input bool ShowThursdayUsa2_1H_MiddleDownBox = false;
input bool ShowThursdayUsa2_4H_TopBox = true;
input bool ShowThursdayUsa2_4H_BottomBox = true;
input bool ShowThursdayUsa2_4H_MiddleUpBox = false;
input bool ShowThursdayUsa2_4H_MiddleDownBox = false;

// جمعه
input  string Friday ="جمعه " ;
input bool DisableFriday = false; // خاموش/روشن کردن جمعه
input string FridayAsia = "یک ساعته و چهار ساعته آسیا"; 
input bool ShowFridayAsia1H_TopBox = true;
input bool ShowFridayAsia1H_BottomBox = true;
input bool ShowFridayAsia1H_MiddleUpBox = true;
input bool ShowFridayAsia1H_MiddleDownBox = true;
input bool ShowFridayAsia4H_TopBox = TRUE;
input bool ShowFridayAsia4H_BottomBox = TRUE;
input bool ShowFridayAsia4H_MiddleUpBox = false;
input bool ShowFridayAsia4H_MiddleDownBox = false;
input  string FridayOuro = "یک ساعته و چهار ساعته اروپا" ;
input bool ShowFridayOuro1H_TopBox = true;
input bool ShowFridayOuro1H_BottomBox = true;
input bool ShowFridayOuro1H_MiddleUpBox = true;
input bool ShowFridayOuro1H_MiddleDownBox = true;
input bool ShowFridayOuro4H_TopBox = true;
input bool ShowFridayOuro4H_BottomBox = true;
input bool ShowFridayOuro4H_MiddleUpBox = false;
input bool ShowFridayOuro4H_MiddleDownBox = false;
input string FridayUsa1 = "یک ساعته و چهار ساعته امریکا 1" ;
input bool ShowFridayUsa1_1H_TopBox = false;
input bool ShowFridayUsa1_1H_BottomBox = false;
input bool ShowFridayUsa1_1H_MiddleUpBox = true;
input bool ShowFridayUsa1_1H_MiddleDownBox = true;
input bool ShowFridayUsa1_4H_TopBox = false;
input bool ShowFridayUsa1_4H_BottomBox = false;
input bool ShowFridayUsa1_4H_MiddleUpBox = false;
input bool ShowFridayUsa1_4H_MiddleDownBox = false;
input string FridayUsa2 = "یک ساعته و چهار ساعته امریکا 2" ;
input bool ShowFridayUsa2_1H_TopBox = false;
input bool ShowFridayUsa2_1H_BottomBox = false;
input bool ShowFridayUsa2_1H_MiddleUpBox = true;
input bool ShowFridayUsa2_1H_MiddleDownBox = true;
input bool ShowFridayUsa2_4H_TopBox = true;
input bool ShowFridayUsa2_4H_BottomBox = true;
input bool ShowFridayUsa2_4H_MiddleUpBox = false;
input bool ShowFridayUsa2_4H_MiddleDownBox = false;


//+------------------------------------------------------------------+
//| Custom indicator initialization function                          |
//+------------------------------------------------------------------+
int OnInit() {
    return(INIT_SUCCEEDED);
}

//+------------------------------------------------------------------+
//| Custom indicator deinitialization function                       |
//+------------------------------------------------------------------+
void OnDeinit(const int reason) {
    if (reason == REASON_REMOVE) {
        ObjectsDeleteAll(0, "Box_");
    }
}

//+------------------------------------------------------------------+
//| Custom indicator iteration function                               |
//+------------------------------------------------------------------+
int OnCalculate(const int rates_total,
                const int prev_calculated,
                const datetime &time[],
                const double &open[],
                const double &high[],
                const double &low[],
                const double &close[],
                const long &tick_volume[],
                const long &volume[],
                const int &spread[]) {

    if (rates_total == prev_calculated) return rates_total;

    if (prev_calculated == 0) ObjectsDeleteAll(0, "Box_");

    datetime today = TimeCurrent();
    datetime dateStart = today - DaysBack * 86400;

    for (int setIndex = 1; setIndex <= 4; setIndex++) {
        datetime currentDay;
        int dayOfWeek;

        for (int dayOffset = 0; dayOffset <= DaysBack; dayOffset++) {
            currentDay = dateStart + dayOffset * 86400;
            dayOfWeek = TimeDayOfWeek(currentDay);

            // تنظیم زمان شروع و پایان برای هر سشن
            string StartTime, EndTime;
            int DistanceFromTopfor1hours, DistanceFromBottomfor1hours, BoxThicknessfor1hours;
            color BoxColor1hours, MiddleBoxColor1hours;
            bool ShowTopBox1hours, ShowBottomBox1hours, ShowMiddleBoxUp1hours, ShowMiddleBoxDown1hours;

            int DistanceFromTopfor4hours, DistanceFromBottomfor4hours, BoxThicknessfor4hours;
            color BoxColor4hours, MiddleBoxColor4hours;
            bool ShowTopBox4hours, ShowBottomBox4hours, ShowMiddleBoxUp4hours, ShowMiddleBoxDown4hours;

            // تنظیمات برای هر سشن بر اساس اندیس setIndex
            switch (setIndex) {
                case 1: // سشن آسیا
                    StartTime = StartTimeAsia;
                    EndTime = EndTimeAsia;
                    DistanceFromTopfor1hours = DistanceFromTopfor1hoursAsia;
                    DistanceFromBottomfor1hours = DistanceFromBottomfor1hoursAsia;
                    BoxThicknessfor1hours = BoxThicknessfor1hoursAsia;
                    BoxColor1hours = BoxColor1hoursAsia;
                    MiddleBoxColor1hours = MiddleBoxColor1hoursAsia;

                    DistanceFromTopfor4hours = DistanceFromTopfor4hoursAsia;
                    DistanceFromBottomfor4hours = DistanceFromBottomfor4hoursAsia;
                    BoxThicknessfor4hours = BoxThicknessfor4hoursAsia;
                    BoxColor4hours = BoxColor4hoursAsia;
                    MiddleBoxColor4hours = MiddleBoxColor4hoursAsia;

                    // بررسی وضعیت خاموش کردن دوشنبه
                    if (dayOfWeek == 1 && DisableMonday) continue;

                    // تعیین فعال یا غیرفعال بودن هر باکس برای دوشنبه
                    if (dayOfWeek == 1) {
                        ShowTopBox1hours = ShowMondayAsia1H_TopBox;
                        ShowBottomBox1hours = ShowMondayAsia1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowMondayAsia1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowMondayAsia1H_MiddleDownBox;

                        ShowTopBox4hours = ShowMondayAsia4H_TopBox;
                        ShowBottomBox4hours = ShowMondayAsia4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowMondayAsia4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowMondayAsia4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای سه‌شنبه
                    else if (dayOfWeek == 2) {
                        if (DisableTuesday) continue;
                        ShowTopBox1hours = ShowTuesdayAsia1H_TopBox;
                        ShowBottomBox1hours = ShowTuesdayAsia1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowTuesdayAsia1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowTuesdayAsia1H_MiddleDownBox;

                        ShowTopBox4hours = ShowTuesdayAsia4H_TopBox;
                        ShowBottomBox4hours = ShowTuesdayAsia4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowTuesdayAsia4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowTuesdayAsia4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای چهارشنبه
                    else if (dayOfWeek == 3) {
                        if (DisableWednesday) continue;
                        ShowTopBox1hours = ShowWednesdayAsia1H_TopBox;
                        ShowBottomBox1hours = ShowWednesdayAsia1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowWednesdayAsia1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowWednesdayAsia1H_MiddleDownBox;

                        ShowTopBox4hours = ShowWednesdayAsia4H_TopBox;
                        ShowBottomBox4hours = ShowWednesdayAsia4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowWednesdayAsia4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowWednesdayAsia4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای پنج‌شنبه
                    else if (dayOfWeek == 4) {
                        if (DisableThursday) continue;
                        ShowTopBox1hours = ShowThursdayAsia1H_TopBox;
                        ShowBottomBox1hours = ShowThursdayAsia1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowThursdayAsia1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowThursdayAsia1H_MiddleDownBox;

                        ShowTopBox4hours = ShowThursdayAsia4H_TopBox;
                        ShowBottomBox4hours = ShowThursdayAsia4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowThursdayAsia4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowThursdayAsia4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای جمعه
                    else if (dayOfWeek == 5) {
                        if (DisableFriday) continue;
                        ShowTopBox1hours = ShowFridayAsia1H_TopBox;
                        ShowBottomBox1hours = ShowFridayAsia1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowFridayAsia1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowFridayAsia1H_MiddleDownBox;

                        ShowTopBox4hours = ShowFridayAsia4H_TopBox;
                        ShowBottomBox4hours = ShowFridayAsia4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowFridayAsia4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowFridayAsia4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای شنبه
                   
                    break;

                case 2: // سشن اروپا (Ouro)
                    StartTime = StartTimeOuro;
                    EndTime = EndTimeOuro;
                    DistanceFromTopfor1hours = DistanceFromTopfor1hoursOuro;
                    DistanceFromBottomfor1hours = DistanceFromBottomfor1hoursOuro;
                    BoxThicknessfor1hours = BoxThicknessfor1hoursOuro;
                    BoxColor1hours = BoxColor1hoursOuro;
                    MiddleBoxColor1hours = MiddleBoxColor1hoursOuro;

                    DistanceFromTopfor4hours = DistanceFromTopfor4hoursOuro;
                    DistanceFromBottomfor4hours = DistanceFromBottomfor4hoursOuro;
                    BoxThicknessfor4hours = BoxThicknessfor4hoursOuro;
                    BoxColor4hours = BoxColor4hoursOuro;
                    MiddleBoxColor4hours = MiddleBoxColor4hoursOuro;

                    // بررسی وضعیت خاموش کردن دوشنبه
                    if (dayOfWeek == 1 && DisableMonday) continue;

                    // تعیین فعال یا غیرفعال بودن هر باکس برای دوشنبه
                    if (dayOfWeek == 1) {
                        ShowTopBox1hours = ShowMondayOuro1H_TopBox;
                        ShowBottomBox1hours = ShowMondayOuro1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowMondayOuro1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowMondayOuro1H_MiddleDownBox;

                        ShowTopBox4hours = ShowMondayOuro4H_TopBox;
                        ShowBottomBox4hours = ShowMondayOuro4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowMondayOuro4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowMondayOuro4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای سه‌شنبه
                    else if (dayOfWeek == 2) {
                        if (DisableTuesday) continue;
                        ShowTopBox1hours = ShowTuesdayOuro1H_TopBox;
                        ShowBottomBox1hours = ShowTuesdayOuro1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowTuesdayOuro1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowTuesdayOuro1H_MiddleDownBox;

                        ShowTopBox4hours = ShowTuesdayOuro4H_TopBox;
                        ShowBottomBox4hours = ShowTuesdayOuro4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowTuesdayOuro4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowTuesdayOuro4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای چهارشنبه
                    else if (dayOfWeek == 3) {
                        if (DisableWednesday) continue;
                        ShowTopBox1hours = ShowWednesdayOuro1H_TopBox;
                        ShowBottomBox1hours = ShowWednesdayOuro1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowWednesdayOuro1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowWednesdayOuro1H_MiddleDownBox;

                        ShowTopBox4hours = ShowWednesdayOuro4H_TopBox;
                        ShowBottomBox4hours = ShowWednesdayOuro4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowWednesdayOuro4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowWednesdayOuro4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای پنج‌شنبه
                    else if (dayOfWeek == 4) {
                        if (DisableThursday) continue;
                        ShowTopBox1hours = ShowThursdayOuro1H_TopBox;
                        ShowBottomBox1hours = ShowThursdayOuro1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowThursdayOuro1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowThursdayOuro1H_MiddleDownBox;

                        ShowTopBox4hours = ShowThursdayOuro4H_TopBox;
                        ShowBottomBox4hours = ShowThursdayOuro4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowThursdayOuro4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowThursdayOuro4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای جمعه
                    else if (dayOfWeek == 5) {
                        if (DisableFriday) continue;
                        ShowTopBox1hours = ShowFridayOuro1H_TopBox;
                        ShowBottomBox1hours = ShowFridayOuro1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowFridayOuro1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowFridayOuro1H_MiddleDownBox;

                        ShowTopBox4hours = ShowFridayOuro4H_TopBox;
                        ShowBottomBox4hours = ShowFridayOuro4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowFridayOuro4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowFridayOuro4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای شنبه
                    
                    break;

                case 3: // سشن آمریکا 1
                    StartTime = StartTimeUsa1;
                    EndTime = EndTimeUsa1;
                    DistanceFromTopfor1hours = DistanceFromTopfor1hoursUsa1;
                    DistanceFromBottomfor1hours = DistanceFromBottomfor1hoursUsa1;
                    BoxThicknessfor1hours = BoxThicknessfor1hoursUsa1;
                    BoxColor1hours = BoxColor1hoursUsa1;
                    MiddleBoxColor1hours = MiddleBoxColor1hoursUsa1;

                    DistanceFromTopfor4hours = DistanceFromTopfor4hoursUsa1;
                    DistanceFromBottomfor4hours = DistanceFromBottomfor4hoursUsa1;
                    BoxThicknessfor4hours = BoxThicknessfor4hoursUsa1;
                    BoxColor4hours = BoxColor4hoursUsa1;
                    MiddleBoxColor4hours = MiddleBoxColor4hoursUsa1;

                    // بررسی وضعیت خاموش کردن دوشنبه
                    if (dayOfWeek == 1 && DisableMonday) continue;

                    // تعیین فعال یا غیرفعال بودن هر باکس برای دوشنبه
                    if (dayOfWeek == 1) {
                        ShowTopBox1hours = ShowMondayUsa1_1H_TopBox;
                        ShowBottomBox1hours = ShowMondayUsa1_1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowMondayUsa1_1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowMondayUsa1_1H_MiddleDownBox;

                        ShowTopBox4hours = ShowMondayUsa1_4H_TopBox;
                        ShowBottomBox4hours = ShowMondayUsa1_4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowMondayUsa1_4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowMondayUsa1_4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای سه‌شنبه
                    else if (dayOfWeek == 2) {
                        if (DisableTuesday) continue;
                        ShowTopBox1hours = ShowTuesdayUsa1_1H_TopBox;
                        ShowBottomBox1hours = ShowTuesdayUsa1_1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowTuesdayUsa1_1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowTuesdayUsa1_1H_MiddleDownBox;

                        ShowTopBox4hours = ShowTuesdayUsa1_4H_TopBox;
                        ShowBottomBox4hours = ShowTuesdayUsa1_4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowTuesdayUsa1_4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowTuesdayUsa1_4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای چهارشنبه
                    else if (dayOfWeek == 3) {
                        if (DisableWednesday) continue;
                        ShowTopBox1hours = ShowWednesdayUsa1_1H_TopBox;
                        ShowBottomBox1hours = ShowWednesdayUsa1_1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowWednesdayUsa1_1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowWednesdayUsa1_1H_MiddleDownBox;

                        ShowTopBox4hours = ShowWednesdayUsa1_4H_TopBox;
                        ShowBottomBox4hours = ShowWednesdayUsa1_4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowWednesdayUsa1_4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowWednesdayUsa1_4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای پنج‌شنبه
                    else if (dayOfWeek == 4) {
                        if (DisableThursday) continue;
                        ShowTopBox1hours = ShowThursdayUsa1_1H_TopBox;
                        ShowBottomBox1hours = ShowThursdayUsa1_1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowThursdayUsa1_1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowThursdayUsa1_1H_MiddleDownBox;

                        ShowTopBox4hours = ShowThursdayUsa1_4H_TopBox;
                        ShowBottomBox4hours = ShowThursdayUsa1_4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowThursdayUsa1_4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowThursdayUsa1_4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای جمعه
                    else if (dayOfWeek == 5) {
                        if (DisableFriday) continue;
                        ShowTopBox1hours = ShowFridayUsa1_1H_TopBox;
                        ShowBottomBox1hours = ShowFridayUsa1_1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowFridayUsa1_1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowFridayUsa1_1H_MiddleDownBox;

                        ShowTopBox4hours = ShowFridayUsa1_4H_TopBox;
                        ShowBottomBox4hours = ShowFridayUsa1_4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowFridayUsa1_4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowFridayUsa1_4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای شنبه
                   
                    break;

                case 4: // سشن آمریکا 2
                    StartTime = StartTimeUsa2;
                    EndTime = EndTimeUsa2;
                    DistanceFromTopfor1hours = DistanceFromTopfor1hoursUsa2;
                    DistanceFromBottomfor1hours = DistanceFromBottomfor1hoursUsa2;
                    BoxThicknessfor1hours = BoxThicknessfor1hoursUsa2;
                    BoxColor1hours = BoxColor1hoursUsa2;
                    MiddleBoxColor1hours = MiddleBoxColor1hoursUsa2;

                    DistanceFromTopfor4hours = DistanceFromTopfor4hoursUsa2;
                    DistanceFromBottomfor4hours = DistanceFromBottomfor4hoursUsa2;
                    BoxThicknessfor4hours = BoxThicknessfor4hoursUsa2;
                    BoxColor4hours = BoxColor4hoursUsa2;
                    MiddleBoxColor4hours = MiddleBoxColor4hoursUsa2;

                    // بررسی وضعیت خاموش کردن دوشنبه
                    if (dayOfWeek == 1 && DisableMonday) continue;

                    // تعیین فعال یا غیرفعال بودن هر باکس برای دوشنبه
                    if (dayOfWeek == 1) {
                        ShowTopBox1hours = ShowMondayUsa2_1H_TopBox;
                        ShowBottomBox1hours = ShowMondayUsa2_1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowMondayUsa2_1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowMondayUsa2_1H_MiddleDownBox;

                        ShowTopBox4hours = ShowMondayUsa2_4H_TopBox;
                        ShowBottomBox4hours = ShowMondayUsa2_4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowMondayUsa2_4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowMondayUsa2_4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای سه‌شنبه
                    else if (dayOfWeek == 2) {
                        if (DisableTuesday) continue;
                        ShowTopBox1hours = ShowTuesdayUsa2_1H_TopBox;
                        ShowBottomBox1hours = ShowTuesdayUsa2_1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowTuesdayUsa2_1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowTuesdayUsa2_1H_MiddleDownBox;

                        ShowTopBox4hours = ShowTuesdayUsa2_4H_TopBox;
                        ShowBottomBox4hours = ShowTuesdayUsa2_4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowTuesdayUsa2_4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowTuesdayUsa2_4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای چهارشنبه
                    else if (dayOfWeek == 3) {
                        if (DisableWednesday) continue;
                        ShowTopBox1hours = ShowWednesdayUsa2_1H_TopBox;
                        ShowBottomBox1hours = ShowWednesdayUsa2_1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowWednesdayUsa2_1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowWednesdayUsa2_1H_MiddleDownBox;

                        ShowTopBox4hours = ShowWednesdayUsa2_4H_TopBox;
                        ShowBottomBox4hours = ShowWednesdayUsa2_4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowWednesdayUsa2_4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowWednesdayUsa2_4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای پنج‌شنبه
                    else if (dayOfWeek == 4) {
                        if (DisableThursday) continue;
                        ShowTopBox1hours = ShowThursdayUsa2_1H_TopBox;
                        ShowBottomBox1hours = ShowThursdayUsa2_1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowThursdayUsa2_1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowThursdayUsa2_1H_MiddleDownBox;

                        ShowTopBox4hours = ShowThursdayUsa2_4H_TopBox;
                        ShowBottomBox4hours = ShowThursdayUsa2_4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowThursdayUsa2_4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowThursdayUsa2_4H_MiddleDownBox;
                    }
                    // تعیین فعال یا غیرفعال بودن هر باکس برای جمعه
                    else if (dayOfWeek == 5) {
                        if (DisableFriday) continue;
                        ShowTopBox1hours = ShowFridayUsa2_1H_TopBox;
                        ShowBottomBox1hours = ShowFridayUsa2_1H_BottomBox;
                        ShowMiddleBoxUp1hours = ShowFridayUsa2_1H_MiddleUpBox;
                        ShowMiddleBoxDown1hours = ShowFridayUsa2_1H_MiddleDownBox;

                        ShowTopBox4hours = ShowFridayUsa2_4H_TopBox;
                        ShowBottomBox4hours = ShowFridayUsa2_4H_BottomBox;
                        ShowMiddleBoxUp4hours = ShowFridayUsa2_4H_MiddleUpBox;
                        ShowMiddleBoxDown4hours = ShowFridayUsa2_4H_MiddleDownBox;
                    }
                 
                    break;
            }

            // تجزیه زمان شروع و پایان
            int StartHour, StartMinute;
            int EndHour, EndMinute;
            StringToTime(StartTime, StartHour, StartMinute);
            StringToTime(EndTime, EndHour, EndMinute);

            datetime startTime = StrToTime(TimeToString(currentDay, TIME_DATE) + " " + IntegerToString(StartHour) + ":" + IntegerToString(StartMinute));
            datetime endTime = StrToTime(TimeToString(currentDay, TIME_DATE) + " " + IntegerToString(EndHour) + ":" + IntegerToString(EndMinute));

            if (today < endTime) {
                continue; // اگر هنوز به زمان پایان نرسیده‌ایم، هیچ باکسی رسم نخواهد شد
            }

            double highestPrice = DBL_MIN;
            double lowestPrice = DBL_MAX;

            for (int i = 0; i < rates_total; i++) {
                if (time[i] >= startTime && time[i] <= endTime) {
                    highestPrice = MathMax(highestPrice, high[i]);
                    lowestPrice = MathMin(lowestPrice, low[i]);
                }
            }

            if (highestPrice != DBL_MIN && lowestPrice != DBL_MAX) {
                string boxBaseName = "Box_" + TimeToString(currentDay, TIME_DATE) + "_Set" + IntegerToString(setIndex);

                datetime boxStartTime = endTime + 60; // یک دقیقه بعد از زمان پایان
                datetime boxEndTime = StrToTime(TimeToString(currentDay, TIME_DATE) + " 23:59:00");

                // باکس‌های پایین
                if (ShowTopBox1hours) {
                    ObjectCreate(0, boxBaseName + "پایین انتها یک ساعته" , OBJ_RECTANGLE, 0, boxStartTime, highestPrice - DistanceFromTopfor1hours * Point,boxStartTime+6*3600, highestPrice - BoxThicknessfor1hours * Point);
                    ObjectSetInteger(0, boxBaseName + "پایین انتها یک ساعته", OBJPROP_COLOR, BoxColor1hours);
                    ObjectSetInteger(0, boxBaseName + "پایین انتها یک ساعته" , OBJPROP_WIDTH, 1);
                     ObjectSetInteger(0, boxBaseName+ "پایین انتها یک ساعته", OBJPROP_BACK, False);
                   if (ShowLineStopLevel) {
                    // رسم خط در بالای باکس با فاصله تعیین‌شده
                    ObjectCreate(0, boxBaseName + "استاپ پایین انتها یک ساعته" , OBJ_TREND, 0, boxStartTime, highestPrice - (DistanceFromTopfor1hours + LineStopLevel) * Point, boxStartTime+4*3600, highestPrice - (DistanceFromTopfor1hours + LineStopLevel) * Point);
                    ObjectSetInteger(0, boxBaseName + "استاپ پایین انتها یک ساعته" , OBJPROP_COLOR, BoxColor1hours);
                    ObjectSetInteger(0, boxBaseName + "استاپ پایین انتها یک ساعته" , OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + "استاپ پایین انتها یک ساعته" , OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + "استاپ پایین انتها یک ساعته" , OBJPROP_STYLE, STYLE_DOT);  // تنظیم به صورت نقطه‌چین
                    }
                      if (ShowLinebreakEven) {
                               //رسم خط بریک ایون
                    ObjectCreate(0, boxBaseName + "بریک ایون یایین انتها یک ساعته"  , OBJ_TREND, 0, boxStartTime, highestPrice - (DistanceFromTopfor1hours - LinebreakEven) * Point, boxStartTime+4*3600, highestPrice - (DistanceFromTopfor1hours - LinebreakEven) * Point);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون یایین انتها یک ساعته" , OBJPROP_COLOR, BoxColorBreakEven);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون یایین انتها یک ساعته" , OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون یایین انتها یک ساعته" , OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون یایین انتها یک ساعته" , OBJPROP_STYLE, STYLE_DASHDOTDOT);  // تنظیم به صورت نقطه‌چین
                    }
                     if (ShowTP) {
                      //رسم خط TP
                    ObjectCreate(0, boxBaseName + " تی پی یایین انتها یک ساعته"  , OBJ_TREND, 0, boxStartTime, highestPrice - (DistanceFromTopfor1hours - TP) * Point, boxStartTime+4*3600, highestPrice - (DistanceFromTopfor1hours - TP) * Point);
                    ObjectSetInteger(0, boxBaseName + " تی پی یایین انتها یک ساعته" , OBJPROP_COLOR, BoxTP);
                    ObjectSetInteger(0, boxBaseName +  " تی پی یایین انتها یک ساعته" , OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName +  " تی پی یایین انتها یک ساعته" , OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + " تی پی یایین انتها یک ساعته" , OBJPROP_STYLE, STYLE_DASH);  // تنظیم به صورت نقطه‌چین
                        }
                         }

               
                // باکس‌های بالا
                if (ShowBottomBox1hours) {
                    ObjectCreate(0, boxBaseName + "بالا انتها یک ساعته", OBJ_RECTANGLE, 0, boxStartTime, lowestPrice + DistanceFromBottomfor1hours * Point,boxStartTime+6*3600, lowestPrice + BoxThicknessfor1hours * Point);
                    ObjectSetInteger(0, boxBaseName + "بالا انتها یک ساعته", OBJPROP_COLOR, BoxColor1hours);
                    ObjectSetInteger(0, boxBaseName + "بالا انتها یک ساعته", OBJPROP_WIDTH,1);
                     ObjectSetInteger(0, boxBaseName + "بالا انتها یک ساعته", OBJPROP_BACK, False);
                      if (ShowLineStopLevel) {
                     //رسم خط پایین
                    ObjectCreate(0, boxBaseName + " استاپ بالا انتها یک ساعته", OBJ_TREND, 0, boxStartTime,lowestPrice + (DistanceFromBottomfor1hours + LineStopLevel) * Point, boxStartTime+4*3600, lowestPrice +  (DistanceFromBottomfor1hours + LineStopLevel) * Point);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا انتها یک ساعته", OBJPROP_COLOR, BoxColor1hours);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا انتها یک ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا انتها یک ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا انتها یک ساعته", OBJPROP_STYLE, STYLE_DOT);  // تنظیم به صورت نقطه‌چین
                    }
                     if (ShowLinebreakEven) {
                   //رسم خط بریک ایون
                    ObjectCreate(0, boxBaseName + "بریک ایون بالا انتها یک ساعته", OBJ_TREND, 0, boxStartTime,lowestPrice + (DistanceFromBottomfor1hours - LinebreakEven) * Point, boxStartTime+4*3600, lowestPrice +  (DistanceFromBottomfor1hours - LinebreakEven) * Point);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا انتها یک ساعته", OBJPROP_COLOR, BoxColorBreakEven);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا انتها یک ساعته" , OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا انتها یک ساعته" , OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا انتها یک ساعته" , OBJPROP_STYLE, STYLE_DASHDOTDOT);  // تنظیم به صورت نقطه‌چین
                    }
                      if (ShowTP) {
                    // TP
                    ObjectCreate(0, boxBaseName + " تی پی بالا انتها یک ساعته", OBJ_TREND, 0, boxStartTime,lowestPrice + (DistanceFromBottomfor1hours - TP) * Point, boxStartTime+4*3600, lowestPrice +  (DistanceFromBottomfor1hours - TP) * Point);
                    ObjectSetInteger(0, boxBaseName + " تی پی بالا انتها یک ساعته" , OBJPROP_COLOR, BoxTP);
                    ObjectSetInteger(0, boxBaseName + " تی پی بالا انتها یک ساعته", OBJPROP_WIDTH,1);
                    ObjectSetInteger(0, boxBaseName + " تی پی بالا انتها یک ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + " تی پی بالا انتها یک ساعته", OBJPROP_STYLE, STYLE_DASH);  // تنظیم به صورت نقطه‌چین
                }
                }
                

                // محاسبه قیمت میانیی یکبار
                double middlePrice = (highestPrice + lowestPrice) / 2;

                  // باکس‌های میانه بالا
                if (ShowMiddleBoxUp1hours) {
                    ObjectCreate(0, boxBaseName + "بالا وسط یک ساعته" , OBJ_RECTANGLE, 0, boxStartTime, middlePrice + DistanceFromTopfor1hours * Point, boxStartTime+6*3600, middlePrice + BoxThicknessfor1hours * Point);
                    ObjectSetInteger(0, boxBaseName + "بالا وسط یک ساعته" , OBJPROP_COLOR, MiddleBoxColor1hours);
                    ObjectSetInteger(0, boxBaseName + "بالا وسط یک ساعته" ,  OBJPROP_WIDTH,1);
                     ObjectSetInteger(0, boxBaseName + "بالا وسط یک ساعته" , OBJPROP_BACK, False);
                      if (ShowLineStopLevel) {
                      // رسم خط میانه 
                    ObjectCreate(0, boxBaseName + " استاپ بالا وسط یک ساعته", OBJ_TREND, 0, boxStartTime,  middlePrice + (DistanceFromTopfor1hours + LineStopLevel) * Point, boxStartTime+4*3600, middlePrice +(DistanceFromTopfor1hours + LineStopLevel) * Point);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا وسط یک ساعته", OBJPROP_COLOR, MiddleBoxColor1hours);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا وسط یک ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا وسط یک ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا وسط یک ساعته", OBJPROP_STYLE, STYLE_DOT);  // تنظیم به صورت نقطه‌چین
                    }
                     if (ShowLinebreakEven) {
                      // رسم خط بریک 
                    ObjectCreate(0, boxBaseName + "بریک ایون بالا وسط یک ساعته" , OBJ_TREND, 0, boxStartTime,  middlePrice + (DistanceFromTopfor1hours - LinebreakEven) * Point, boxStartTime+4*3600, middlePrice +(DistanceFromTopfor1hours - LinebreakEven) * Point);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا وسط یک ساعته" , OBJPROP_COLOR, BoxColorBreakEven);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا وسط یک ساعته" ,  OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا وسط یک ساعته" , OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا وسط یک ساعته" , OBJPROP_STYLE, STYLE_DASHDOTDOT);  // تنظیم به صورت نقطه‌چین
                    }
                      if (ShowTP) {
                    // TP
                    ObjectCreate(0, boxBaseName + " تی پی بالا وسط یک ساعته" , OBJ_TREND, 0, boxStartTime,  middlePrice + (DistanceFromTopfor1hours - TP) * Point, boxStartTime+4*3600, middlePrice +(DistanceFromTopfor1hours - TP) * Point);
                     ObjectSetInteger(0, boxBaseName + " تی پی بالا وسط یک ساعته", OBJPROP_COLOR, BoxTP);
                    ObjectSetInteger(0, boxBaseName +  " تی پی بالا وسط یک ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + " تی پی بالا وسط یک ساعته" , OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + " تی پی بالا وسط یک ساعته" , OBJPROP_STYLE, STYLE_DASH);  // تنظیم به صورت نقطه‌چین
               }
                }

                // باکس‌های میانه پایین
                if (ShowMiddleBoxDown1hours) {
                    ObjectCreate(0, boxBaseName + "پایین وسط یک ساعته", OBJ_RECTANGLE, 0, boxStartTime, middlePrice - DistanceFromBottomfor1hours * Point, boxStartTime+6*3600, middlePrice - BoxThicknessfor1hours * Point);
                    ObjectSetInteger(0, boxBaseName + "پایین وسط یک ساعته", OBJPROP_COLOR, MiddleBoxColor1hours);
                    ObjectSetInteger(0, boxBaseName + "پایین وسط یک ساعته", OBJPROP_WIDTH, 1);
                     ObjectSetInteger(0, boxBaseName + "پایین وسط یک ساعته", OBJPROP_BACK, False);
                     if (ShowLineStopLevel) {
                    // خط میانه
                    ObjectCreate(0, boxBaseName + " استاپ پایین وسط یک ساعته", OBJ_TREND, 0, boxStartTime,middlePrice - (DistanceFromBottomfor1hours + LineStopLevel) * Point, boxStartTime+4*3600, middlePrice -  (DistanceFromBottomfor1hours + LineStopLevel) * Point);
                    ObjectSetInteger(0, boxBaseName + " استاپ پایین وسط یک ساعته", OBJPROP_COLOR,MiddleBoxColor1hours);
                    ObjectSetInteger(0, boxBaseName + " استاپ پایین وسط یک ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + " استاپ پایین وسط یک ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + " استاپ پایین وسط یک ساعته", OBJPROP_STYLE, STYLE_DOT);  // تنظیم به صورت نقطه‌چین 
                    }
                     if (ShowLinebreakEven) {
                          // خط بریک ایون
                    ObjectCreate(0, boxBaseName + "بریک ایون پایین وسط یک ساعته", OBJ_TREND, 0, boxStartTime,middlePrice - (DistanceFromBottomfor1hours - LinebreakEven) * Point, boxStartTime+4*3600, middlePrice -  (DistanceFromBottomfor1hours - LinebreakEven) * Point);
                    ObjectSetInteger(0, boxBaseName +"بریک ایون پایین وسط یک ساعته", OBJPROP_COLOR,BoxColorBreakEven);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون پایین وسط یک ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون پایین وسط یک ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون پایین وسط یک ساعته", OBJPROP_STYLE, STYLE_DASHDOTDOT);  // تنظیم به صورت نقطه‌چین 
                    }
                      if (ShowTP) {
                       // تی پی
                    ObjectCreate(0, boxBaseName + " تی پی پایین وسط یک ساعته", OBJ_TREND, 0, boxStartTime,middlePrice - (DistanceFromBottomfor1hours - TP) * Point, boxStartTime+4*3600, middlePrice -  (DistanceFromBottomfor1hours - TP) * Point);
                     ObjectSetInteger(0, boxBaseName + " تی پی پایین وسط یک ساعته" , OBJPROP_COLOR, BoxTP);
                    ObjectSetInteger(0, boxBaseName + " تی پی پایین وسط یک ساعته" , OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + " تی پی پایین وسط یک ساعته" , OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName +  " تی پی پایین وسط یک ساعته" , OBJPROP_STYLE, STYLE_DASH);  // تنظیم به صورت نقطه‌چین
               }
                }
        // باکس‌های 4 ساعته
                // باکس‌های 4 ساعته
                if (ShowTopBox4hours) {
                    ObjectCreate(0, boxBaseName + "پایین انتها چهار ساعته", OBJ_RECTANGLE, 0, boxStartTime, highestPrice - DistanceFromTopfor4hours * Point, boxStartTime+6*3600, highestPrice - BoxThicknessfor4hours * Point);
                    ObjectSetInteger(0, boxBaseName + "پایین انتها چهار ساعته", OBJPROP_COLOR, BoxColor4hours);
                    ObjectSetInteger(0, boxBaseName + "پایین انتها چهار ساعته", OBJPROP_WIDTH, 1);
                     ObjectSetInteger(0, boxBaseName + "پایین انتها چهار ساعته", OBJPROP_BACK, False);
                     if (ShowLineStopLevel) {
                      // رسم خط در بالای باکس با فاصله تعیین‌شده
                    ObjectCreate(0, boxBaseName + " استاپ پایین انتها چهار ساعته", OBJ_TREND, 0, boxStartTime, highestPrice - (DistanceFromTopfor4hours + LineStopLevel) * Point, boxStartTime+4*3600, highestPrice - (DistanceFromTopfor4hours + LineStopLevel) * Point);
                    ObjectSetInteger(0, boxBaseName + " استاپ پایین انتها چهار ساعته", OBJPROP_COLOR, BoxColor4hours);
                    ObjectSetInteger(0, boxBaseName + " استاپ پایین انتها چهار ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + " استاپ پایین انتها چهار ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + " استاپ پایین انتها چهار ساعته", OBJPROP_STYLE, STYLE_DOT);  // تنظیم به صورت نقطه‌چین
                    }
                    if (ShowLinebreakEven) {
                  
                     // رسم خط بریک
                    ObjectCreate(0, boxBaseName + "بریک ایون پایین انتها چهار ساعته", OBJ_TREND, 0, boxStartTime, highestPrice - (DistanceFromTopfor4hours - LinebreakEven) * Point, boxStartTime+4*3600, highestPrice - (DistanceFromTopfor4hours - LinebreakEven) * Point);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون پایین انتها چهار ساعته", OBJPROP_COLOR, BoxColorBreakEven);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون پایین انتها چهار ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون پایین انتها چهار ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون پایین انتها چهار ساعته", OBJPROP_STYLE, STYLE_DASHDOTDOT);
                    }
                     if (ShowTP) {
                    //تی پی
                    ObjectCreate(0, boxBaseName + " تی پی پایین انتها چهار ساعته", OBJ_TREND, 0, boxStartTime, highestPrice - (DistanceFromTopfor4hours - TP) * Point, boxStartTime+4*3600, highestPrice - (DistanceFromTopfor4hours - TP) * Point);
                     ObjectSetInteger(0, boxBaseName + " تی پی پایین انتها چهار ساعته", OBJPROP_COLOR, BoxTP);
                    ObjectSetInteger(0, boxBaseName + " تی پی پایین انتها چهار ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + " تی پی پایین انتها چهار ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + " تی پی پایین انتها چهار ساعته", OBJPROP_STYLE, STYLE_DASH); 
                    } 
                }

                 // باکس‌های پایین
                if (ShowBottomBox4hours) {
                    ObjectCreate(0, boxBaseName +  "بالا انتها چهار ساعته", OBJ_RECTANGLE, 0, boxStartTime, lowestPrice + DistanceFromBottomfor4hours * Point, boxStartTime+6*3600,lowestPrice + BoxThicknessfor4hours * Point);
                    ObjectSetInteger(0, boxBaseName +  "بالا انتها چهار ساعته", OBJPROP_COLOR, BoxColor4hours);
                    ObjectSetInteger(0, boxBaseName +  "بالا انتها چهار ساعته", OBJPROP_WIDTH,1);
                     ObjectSetInteger(0, boxBaseName +  "بالا انتها چهار ساعته", OBJPROP_BACK, False);
                     if (ShowLineStopLevel) {
                    //رسم خط 
                    ObjectCreate(0, boxBaseName + " استاپ بالا انتها چهار ساعته", OBJ_TREND, 0, boxStartTime,lowestPrice + (DistanceFromBottomfor4hours + LineStopLevel) * Point, boxStartTime+4*3600, lowestPrice +  (DistanceFromBottomfor4hours + LineStopLevel) * Point);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا انتها چهار ساعته", OBJPROP_COLOR, BoxColor4hours);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا انتها چهار ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا انتها چهار ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا انتها چهار ساعته", OBJPROP_STYLE, STYLE_DOT);  // تنظیم به صورت نقطه‌چین
                    }
                   if (ShowLinebreakEven) {
                    //رسم خط بریک
                    ObjectCreate(0, boxBaseName + "بریک ایون بالا انتها چهار ساعته", OBJ_TREND, 0, boxStartTime,lowestPrice + (DistanceFromBottomfor4hours - LinebreakEven) * Point, boxStartTime+4*3600, lowestPrice +  (DistanceFromBottomfor4hours -LinebreakEven) * Point);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا انتها چهار ساعته", OBJPROP_COLOR, BoxColorBreakEven);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا انتها چهار ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا انتها چهار ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا انتها چهار ساعته", OBJPROP_STYLE, STYLE_DASHDOTDOT);  // تنظیم به صورت نقطه‌چین 
                    }
                     if (ShowTP) {
                    //tp
                    ObjectCreate(0, boxBaseName + " تی پی بالا انتها چهار ساعته", OBJ_TREND, 0, boxStartTime,lowestPrice + (DistanceFromBottomfor4hours - TP) * Point, boxStartTime+4*3600, lowestPrice +  (DistanceFromBottomfor4hours -TP) * Point); 
                    ObjectSetInteger(0, boxBaseName + " تی پی بالا انتها چهار ساعته", OBJPROP_COLOR, BoxTP);
                    ObjectSetInteger(0, boxBaseName + " تی پی بالا انتها چهار ساعته", OBJPROP_WIDTH,1);
                    ObjectSetInteger(0, boxBaseName + " تی پی بالا انتها چهار ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + " تی پی بالا انتها چهار ساعته", OBJPROP_STYLE, STYLE_DASH);  // تنظیم به صورت نقطه‌چین 
                }
                }

                // باکس‌های میانه بالا
                                if (ShowMiddleBoxUp4hours) {
                    ObjectCreate(0, boxBaseName + "بالا وسط چهار ساعته", OBJ_RECTANGLE, 0, boxStartTime, middlePrice + DistanceFromTopfor4hours * Point, boxStartTime+6*3600, middlePrice + BoxThicknessfor4hours * Point);
                    ObjectSetInteger(0, boxBaseName + "بالا وسط چهار ساعته", OBJPROP_COLOR, MiddleBoxColor4hours);
                    ObjectSetInteger(0, boxBaseName + "بالا وسط چهار ساعته", OBJPROP_WIDTH,1);
                     ObjectSetInteger(0, boxBaseName + "بالا وسط چهار ساعته", OBJPROP_BACK, False);
                     if (ShowLineStopLevel) {
                  // رسم خط
                    ObjectCreate(0, boxBaseName + " استاپ بالا وسط چهار ساعته", OBJ_TREND, 0, boxStartTime,  middlePrice + (DistanceFromTopfor4hours + LineStopLevel) * Point, boxStartTime+4*3600, middlePrice +(DistanceFromTopfor4hours + LineStopLevel) * Point);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا وسط چهار ساعته", OBJPROP_COLOR, MiddleBoxColor4hours);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا وسط چهار ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا وسط چهار ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + " استاپ بالا وسط چهار ساعته", OBJPROP_STYLE, STYLE_DOT);  // تنظیم به صورت نقطه‌چین
                    }
                    // رسم خط بریک
                    ObjectCreate(0, boxBaseName + "بریک ایون بالا وسط چهار ساعته", OBJ_TREND, 0, boxStartTime,  middlePrice + (DistanceFromTopfor4hours - LinebreakEven) * Point, boxStartTime+4*3600, middlePrice +(DistanceFromTopfor4hours - LinebreakEven) * Point);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا وسط چهار ساعته", OBJPROP_COLOR, BoxColorBreakEven);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا وسط چهار ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا وسط چهار ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName + "بریک ایون بالا وسط چهار ساعته", OBJPROP_STYLE, STYLE_DASHDOTDOT);  // تنظیم به صورت نقطه‌چین
                    if (ShowTP) {
                    // TP
                    ObjectCreate(0, boxBaseName + " تی پی بالا وسط چهار ساعته", OBJ_TREND, 0, boxStartTime,  middlePrice + (DistanceFromTopfor4hours - TP) * Point, boxStartTime+4*3600, middlePrice +(DistanceFromTopfor4hours - TP) * Point);
                     ObjectSetInteger(0, boxBaseName +" تی پی بالا وسط چهار ساعته", OBJPROP_COLOR, BoxTP);
                    ObjectSetInteger(0, boxBaseName +" تی پی بالا وسط چهار ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName +" تی پی بالا وسط چهار ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName +" تی پی بالا وسط چهار ساعته", OBJPROP_STYLE, STYLE_DASH);  // تنظیم به صورت نقطه‌چین
                }
                }

                 // باکس‌های میانه پایین
                if (ShowMiddleBoxDown4hours) {
                    ObjectCreate(0, boxBaseName + "پایین وسط چهار ساعته", OBJ_RECTANGLE, 0, boxStartTime, middlePrice - DistanceFromBottomfor4hours * Point, boxStartTime+6*3600, middlePrice - BoxThicknessfor4hours * Point);
                    ObjectSetInteger(0, boxBaseName + "پایین وسط چهار ساعته", OBJPROP_COLOR, MiddleBoxColor4hours);
                    ObjectSetInteger(0, boxBaseName + "پایین وسط چهار ساعته", OBJPROP_WIDTH, 1);
                     ObjectSetInteger(0, boxBaseName + "پایین وسط چهار ساعته", OBJPROP_BACK, False);
                     if (ShowLineStopLevel) {
                   // رسم خط
                    ObjectCreate(0, boxBaseName +" استاپ پایین وسط چهار ساعته", OBJ_TREND, 0, boxStartTime,middlePrice - (DistanceFromBottomfor4hours + LineStopLevel) * Point, boxStartTime+4*3600, middlePrice -  (DistanceFromBottomfor4hours + LineStopLevel) * Point);
                    ObjectSetInteger(0, boxBaseName +" استاپ پایین وسط چهار ساعته", OBJPROP_COLOR,MiddleBoxColor1hours);
                    ObjectSetInteger(0, boxBaseName +" استاپ پایین وسط چهار ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName +" استاپ پایین وسط چهار ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName +" استاپ پایین وسط چهار ساعته", OBJPROP_STYLE, STYLE_DOT);  // تنظیم به صورت نقطه‌چین
                    }
                    if (ShowLinebreakEven) {
                          // رسم خط بریک
                    ObjectCreate(0, boxBaseName +"بریک ایون پایین وسط چهار ساعته", OBJ_TREND, 0, boxStartTime,middlePrice - (DistanceFromBottomfor4hours - LinebreakEven) * Point, boxStartTime+4*3600, middlePrice -  (DistanceFromBottomfor4hours - LinebreakEven) * Point);
                    ObjectSetInteger(0, boxBaseName +"بریک ایون پایین وسط چهار ساعته", OBJPROP_COLOR,BoxColorBreakEven);
                    ObjectSetInteger(0, boxBaseName +"بریک ایون پایین وسط چهار ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName +"بریک ایون پایین وسط چهار ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName +"بریک ایون پایین وسط چهار ساعته", OBJPROP_STYLE, STYLE_DASHDOTDOT);  // تنظیم به صورت نقطه‌چین
                    }
                     if (ShowTP) {
                     //TP
                    ObjectCreate(0, boxBaseName +" تی پی پایین وسط چهار ساعته", OBJ_TREND, 0, boxStartTime,middlePrice - (DistanceFromBottomfor4hours - TP) * Point, boxStartTime+4*3600, middlePrice -  (DistanceFromBottomfor4hours - TP) * Point);
                    ObjectSetInteger(0, boxBaseName +" تی پی پایین وسط چهار ساعته", OBJPROP_COLOR,BoxTP);
                    ObjectSetInteger(0, boxBaseName +" تی پی پایین وسط چهار ساعته", OBJPROP_WIDTH, 1);
                    ObjectSetInteger(0, boxBaseName +" تی پی پایین وسط چهار ساعته", OBJPROP_RAY_RIGHT, FALSE);
                    ObjectSetInteger(0, boxBaseName +" تی پی پایین وسط چهار ساعته", OBJPROP_STYLE, STYLE_DASH);  // تنظیم به صورت نقطه‌چین
                    }
                    }
            }
        }
    }

    return rates_total;
}
// تابع برای تجزیه زمان به ساعت و دقیقه
void StringToTime(string timeStr, int &hour, int &minute) {
    string hourStr = StringSubstr(timeStr, 0, 2);
    string minuteStr = StringSubstr(timeStr, 3, 2);
    hour = StringToInteger(hourStr);
    minute = StringToInteger(minuteStr);
}

//+------------------------------------------------------------------+
