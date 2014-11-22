//+------------------------------------------------------------------+
//|                                             SunExpert ver0.1.mq4 |
//|                                                Alexander Strokov |
//|                                    strokovalexander.fx@gmail.com |
//+------------------------------------------------------------------+
#property copyright "Alexander Strokov"
#property link      "strokovalexander.fx@gmail.com"
#property version   "0.3"
#property strict
//+------------------------------------------------------------------+
//| Expert initialization function                                   |
//+------------------------------------------------------------------+
extern string Пapаметры="Настройки советника";
extern int LotsBuy=8;
extern int LotsSell=7;
extern bool LimitsOn=true;
extern bool TPnoLots=true;
extern bool TPUpdate=true;
extern string Пapаметры1="Параметры ордеров";
extern bool BuyTrade=true;
extern bool SellTrade=true;
extern int TP=10;
extern int Magic_Number=3213;
extern string Пapаметры2="Уровни открытия ордеров Buy";
extern double LevelBuy1=100;
extern double LevelBuy2=150;
extern double LevelBuy3=200;
extern double LevelBuy4=250;
extern double LevelBuy5=300;
extern double LevelBuy6=350;
extern double LevelBuy7=400;
extern double LevelBuy8=450;
extern double LevelBuy9=500;
extern double LevelBuy10=550;
extern double LevelBuy11=600;
extern double LevelBuy12=700;
extern double LevelBuy13=800;
extern double LevelBuy14=850;
extern double LevelBuy15=900;
extern double LevelBuy16=1000;
extern double LevelBuy17=1100;
extern double LevelBuy18=1200;
extern double LevelBuy19=1300;
extern double LevelBuy20=1400;
extern string Пapаметры3="Уровни открытия ордеров Sell";
extern double LevelSell1=100;
extern double LevelSell2=150;
extern double LevelSell3=200;
extern double LevelSell4=250;
extern double LevelSell5=300;
extern double LevelSell6=350;
extern double LevelSell7=400;
extern double LevelSell8=450;
extern double LevelSell9=500;
extern double LevelSell10=550;
extern double LevelSell11=600;
extern double LevelSell12=700;
extern double LevelSell13=800;
extern double LevelSell14=850;
extern double LevelSell15=900;
extern double LevelSell16=1000;
extern double LevelSell17=1100;
extern double LevelSell18=1200;
extern double LevelSell19=1300;
extern double LevelSell20=1400;
extern string Пapаметры4="Лоты ордеров Buy";
extern double LotBuy1=0.1;
extern double LotBuy2=0.2;
extern double LotBuy3=0.4;
extern double LotBuy4=0.6;
extern double LotBuy5=0.8;
extern double LotBuy6=1;
extern double LotBuy7=1.2;
extern double LotBuy8=1.4;
extern double LotBuy9=1.6;
extern double LotBuy10=1.8;
extern double LotBuy11=2;
extern double LotBuy12=2.2;
extern double LotBuy13=2.4;
extern double LotBuy14=2.6;
extern double LotBuy15=3;
extern double LotBuy16=3.2;
extern double LotBuy17=3.4;
extern double LotBuy18=3.6;
extern double LotBuy19=3.8;
extern double LotBuy20=4;
extern string Пapаметры5="Лоты ордеров Sell";
extern double LotSell1=0.1;
extern double LotSell2=0.2;
extern double LotSell3=0.4;
extern double LotSell4=0.6;
extern double LotSell5=0.8;
extern double LotSell6=1;
extern double LotSell7=1.2;
extern double LotSell8=1.4;
extern double LotSell9=1.6;
extern double LotSell10=1.8;
extern double LotSell11=2;
extern double LotSell12=2.2;
extern double LotSell13=2.4;
extern double LotSell14=2.6;
extern double LotSell15=3;
extern double LotSell16=3.2;
extern double LotSell17=3.4;
extern double LotSell18=3.6;
extern double LotSell19=3.8;
extern double LotSell20=4;



int k;
bool StartBuyOrders;
bool StartSellOrders;
int CountBuy;
int CountSell;
double TotalSlt;
double TotalBLt;
double OrderSwaps;
double LastBuyPrice;
double LastSellPrice;
double TPB;
double TPS;
int total;
bool SellLimitInTrade;
bool BuyLimitInTrade;
double BuyLimitPrice;
double SellLimitPrice;
int ReCountBuy;
int ReCountSell;

int init()
{


if((Digits==3)||(Digits==5)) { k=10;}
if((Digits==4)||(Digits==2)) { k=1;}
OrdersDel();  
   return(0);
}

int deinit()
{

ObjectDelete("label_object1");
ObjectDelete("label_object2");
ObjectDelete("label_object3");
ObjectDelete("label_object4");
   return(0);
}

int start()
{
 if(IsDemo() == false) { Alert("Неверный счет!");
    Sleep (6000);return(0);}
 //Проверка изменений в советнике   
 ReCountBuy=0;ReCountSell=0;
 for(int in=0;in<OrdersTotal();in++)
   {      if(OrderSelect(in, SELECT_BY_POS)==true){ 
    if ( OrderSymbol() == Symbol()) {
if (OrderType() == OP_BUY ){ReCountBuy=ReCountBuy+1;}
if (OrderType() == OP_SELL ){ReCountSell=ReCountSell+1;}
    }}}   
    
if((CountBuy!=0)&&((ReCountBuy<CountBuy)||(ReCountBuy>CountBuy))){CalculateTotalBuyTP();BuyLimDel();}   

if((CountSell!=0)&&((ReCountSell<CountSell)||(ReCountSell>CountSell))){CalculateTotalSellTP();SellLimDel();}   
    
    
    
    
    
 CountBuy=0;CountSell=0;TotalSlt=0;TotalBLt=0;OrderSwaps=0;total=OrdersTotal();LastBuyPrice=0;LastSellPrice=0;
for(int i=0;i<total;i++)
   {
      // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(i, SELECT_BY_POS)==true){ 
    if ( OrderSymbol() == Symbol()) {
if (OrderType() == OP_BUY ){CountBuy=CountBuy+1;TotalBLt=TotalBLt+OrderLots();}
if (OrderType() == OP_SELL ){CountSell=CountSell+1;TotalSlt=TotalSlt+OrderLots();}
if ((OrderType() == OP_SELL )||(OrderType() == OP_BUY )){OrderSwaps=OrderSwaps+OrderSwap();}
    }}}
    
//#Удаление лимитных ордеров
if (CountBuy==0)
{
for (int iDel=OrdersTotal()-1; iDel>=0; iDel--)
   {
      if (!OrderSelect(iDel,SELECT_BY_POS,MODE_TRADES)) break;
            if ((OrderType()==OP_BUYLIMIT  )&&(OrderMagicNumber() == Magic_Number ))    if (IsTradeAllowed()) { if (OrderDelete(OrderTicket())<0) 
            { 
        Alert("Ошибка удаления ордера № ", GetLastError()); 
      }  
            }
}    
}    
if (CountSell==0)
{
for (int iDelS=OrdersTotal()-1; iDelS>=0; iDelS--)
   {
      if (!OrderSelect(iDelS,SELECT_BY_POS,MODE_TRADES)) break;
            if ((OrderType()==OP_SELLLIMIT  )&&(OrderMagicNumber() == Magic_Number ))    if (IsTradeAllowed()) { if (OrderDelete(OrderTicket())<0) 
            { 
        Alert("Ошибка удаления ордера № ", GetLastError()); 
      }  
            }
}    
} 
//#Поиск общего TP для BUY
if ((CountBuy!=0)&&(CountBuy!=1))
{
double BuyOrderTP=0;
bool CalculateNow=false;
for(int iss=0;iss<OrdersTotal();iss++)
   {
      // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(iss, SELECT_BY_POS)==true){ 
    if ( OrderSymbol() == Symbol()) {
if (OrderType() == OP_BUY ){if(BuyOrderTP==0){BuyOrderTP=OrderTakeProfit();}if (BuyOrderTP!=OrderTakeProfit()){CalculateNow=true;}
}}
    }}
if (CalculateNow==true){CalculateTotalBuyTP();}
}
//#Поиск общего TP для SELL
if ((CountSell!=0)&&(CountSell!=1))
{
double SellOrderTP=0;
bool CalculateNow=false;
for(int is=0;is<OrdersTotal();is++)
   {
      // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(is, SELECT_BY_POS)==true){ 
    if ( OrderSymbol() == Symbol()) {
if (OrderType() == OP_SELL ){if(SellOrderTP==0){SellOrderTP=OrderTakeProfit();}if (SellOrderTP!=OrderTakeProfit()){CalculateNow=true;}
}}
    }}

if (CalculateNow==true){CalculateTotalSellTP();}
}
//#Первый ордер buy
if ((CountBuy==0)&&(BuyTrade==true))
{
Print("Открытие первого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy1,Ask,3*k,NULL,Ask+TP*Point*k,"Sun-LotBuy1-buy(1)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }}

}
//#Первый ордер sell
if ((CountSell==0)&&(SellTrade==true))
{
Print("Открытие первого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell1,Bid,3*k,NULL,Bid-TP*Point*k,"Sun-LotSell1-sell(1)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }}
}

if(LimitsOn==false)
{
//#Второй ордер buy
if ((CountBuy==1)&&(BuyTrade==true))
{
for(int ibuy=0;ibuy<OrdersTotal();ibuy++)
   {
      // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy, SELECT_BY_POS)==true){ 
    if (( OrderSymbol() == Symbol())&&(OrderType() == OP_BUY )) {LastBuyPrice=OrderOpenPrice();
    }}}
if(Ask<(LastBuyPrice-LevelBuy1*k*Point))
{
CalculateBuyTP();
Print("Открытие второго ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy2,Ask,3*k,NULL,TPB,"Sun-LotBuy2-buy(2)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy1=0;ibuy1<OrdersTotal();ibuy1++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy1, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy2-buy(2)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Второй ордер sell
if ((CountSell==1)&&(SellTrade==true))
{
for(int isell=0;isell<OrdersTotal();isell++)
{
      // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderType() == OP_SELL )) 
    {LastSellPrice=OrderOpenPrice();}
      } 
}
if(Bid>(LastSellPrice+LevelSell1*k*Point))
{
CalculateSellTP();
Print("Открытие второго ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell2,Ask,3*k,NULL,TPS,"Sun-LotSell2-sell(2)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
   {    
          for(int isell1=0;isell1<OrdersTotal();isell1++)
    {
      // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell1, SELECT_BY_POS)==true){ 
        if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell2-sell(2)")&&(OrderType() == OP_SELL )) {
        RefreshRates();
        OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
                                                  }
    } 
   }
                     }
}
}


//#Третий ордер buy
if ((CountBuy==2)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy2*k*Point))
{
CalculateBuyTP();
Print("Открытие третьего ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy3,Ask,3*k,NULL,TPB,"Sun-LotBuy3-buy(3)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy2=0;ibuy2<OrdersTotal();ibuy2++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy2, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy3-buy(3)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//Третий ордер sell
if ((CountSell==2)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell2*k*Point))
{
CalculateSellTP();
Print("Открытие третьего ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell3,Ask,3*k,NULL,TPS,"Sun-LotSell3-sell(3)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell2=0;isell2<OrdersTotal();isell2++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell2, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell3-sell(3)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}

//#Четвертый ордер buy
if ((CountBuy==3)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy3*k*Point))
{
CalculateBuyTP();
Print("Открытие четвертого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy4,Ask,3*k,NULL,TPB,"Sun-LotBuy4-buy(4)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy3=0;ibuy3<OrdersTotal();ibuy3++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy3, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy4-buy(4)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Четвертый ордер sell
if ((CountSell==3)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell3*k*Point))
{
CalculateSellTP();
Print("Открытие четвертого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell4,Ask,3*k,NULL,TPS,"Sun-LotSell4-sell(4)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell3=0;isell3<OrdersTotal();isell3++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell3, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell4-sell(4)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}


//#Пятый ордер buy
if ((CountBuy==4)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy4*k*Point))
{
CalculateBuyTP();
Print("Открытие пятого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy5,Ask,3*k,NULL,TPB,"Sun-LotBuy5-buy(5)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy4=0;ibuy4<OrdersTotal();ibuy4++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy4, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy5-buy(5)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Пятый ордер sell
if ((CountSell==4)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell4*k*Point))
{
CalculateSellTP();
Print("Открытие пятого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell5,Ask,3*k,NULL,TPS,"Sun-LotSell5-sell(5)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell4=0;isell4<OrdersTotal();isell4++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell4, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell5-sell(5)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}

//#Шестой ордер buy
if ((CountBuy==5)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy5*k*Point))
{
CalculateBuyTP();
Print("Открытие шестого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy6,Ask,3*k,NULL,TPB,"Sun-LotBuy6-buy(6)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy5=0;ibuy5<OrdersTotal();ibuy5++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy5, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy6-buy(6)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Шестой ордер sell
if ((CountSell==5)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell5*k*Point))
{
CalculateSellTP();
Print("Открытие шестого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell6,Ask,3*k,NULL,TPS,"Sun-LotSell6-sell(6)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell5=0;isell5<OrdersTotal();isell5++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell5, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell6-sell(6)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}
//#Седьмой ордер buy
if ((CountBuy==6)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy6*k*Point))
{
CalculateBuyTP();
Print("Открытие седьмого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy7,Ask,3*k,NULL,TPB,"Sun-LotBuy7-buy(7)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy6=0;ibuy6<OrdersTotal();ibuy6++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy6, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy7-buy(7)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Седьмой ордер sell
if ((CountSell==6)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell6*k*Point))
{
CalculateSellTP();
Print("Открытие седьмого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell7,Ask,3*k,NULL,TPS,"Sun-LotSell7-sell(7)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell6=0;isell6<OrdersTotal();isell6++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell6, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell7-sell(7)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}


//#Восьмой ордер buy
if ((CountBuy==7)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy7*k*Point))
{
CalculateBuyTP();
Print("Открытие восьмого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy8,Ask,3*k,NULL,TPB,"Sun-LotBuy8-buy(8)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy7=0;ibuy7<OrdersTotal();ibuy7++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy7, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy8-buy(8)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Восьмой ордер sell
if ((CountSell==7)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell7*k*Point))
{
CalculateSellTP();
Print("Открытие восьмого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell8,Ask,3*k,NULL,TPS,"Sun-LotSell8-sell(8)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell7=0;isell7<OrdersTotal();isell7++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell7, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell8-sell(8)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}


//#Девятый ордер buy
if ((CountBuy==8)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy8*k*Point))
{
CalculateBuyTP();
Print("Открытие девятого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy9,Ask,3*k,NULL,TPB,"Sun-LotBuy9-buy(9)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy8=0;ibuy8<OrdersTotal();ibuy8++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy8, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy9-buy(9)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Девятый ордер sell
if ((CountSell==8)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell8*k*Point))
{
CalculateSellTP();
Print("Открытие девятого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell9,Ask,3*k,NULL,TPS,"Sun-LotSell9-sell(9)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell8=0;isell8<OrdersTotal();isell8++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell8, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell9-sell(9)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}

//#Десятый ордер buy
if ((CountBuy==9)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy9*k*Point))
{
CalculateBuyTP();
Print("Открытие десятого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy10,Ask,3*k,NULL,TPB,"Sun-LotBuy10-buy(10)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy9=0;ibuy9<OrdersTotal();ibuy9++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy9, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy10-buy(10)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Десятый ордер sell
if ((CountSell==9)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell9*k*Point))
{
CalculateSellTP();
Print("Открытие десятого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell10,Ask,3*k,NULL,TPS,"Sun-LotSell10-sell(10)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell9=0;isell9<OrdersTotal();isell9++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell9, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell10-sell(10)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}


//#Одиннадцатый ордер buy
if ((CountBuy==10)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy10*k*Point))
{
CalculateBuyTP();
Print("Открытие одиннадцатого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy11,Ask,3*k,NULL,TPB,"Sun-LotBuy11-buy(11)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy10=0;ibuy10<OrdersTotal();ibuy10++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy10, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy11-buy(11)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Одиннадцатый ордер sell
if ((CountSell==10)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell10*k*Point))
{
CalculateSellTP();
Print("Открытие одиннадцатого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell11,Ask,3*k,NULL,TPS,"Sun-LotSell11-sell(11)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell10=0;isell10<OrdersTotal();isell10++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell10, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell11-sell(11)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}

//#Двенадцатый ордер buy
if ((CountBuy==11)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy11*k*Point))
{
CalculateBuyTP();
Print("Открытие двенадцатого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy12,Ask,3*k,NULL,TPB,"Sun-LotBuy12-buy(12)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy11=0;ibuy11<OrdersTotal();ibuy11++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy11, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy12-buy(12)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Двенадцатый ордер sell
if ((CountSell==11)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell11*k*Point))
{
CalculateSellTP();
Print("Открытие двенадцатого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell12,Ask,3*k,NULL,TPS,"Sun-LotSell12-sell(12)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell11=0;isell11<OrdersTotal();isell11++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell11, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell12-sell(12)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}

//#Тринадцатый ордер buy
if ((CountBuy==12)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy12*k*Point))
{
CalculateBuyTP();
Print("Открытие тринадцатого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy13,Ask,3*k,NULL,TPB,"Sun-LotBuy13-buy(13)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy12=0;ibuy12<OrdersTotal();ibuy12++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy12, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy13-buy(13)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Тринадцатый ордер sell
if ((CountSell==12)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell12*k*Point))
{
CalculateSellTP();
Print("Открытие тринадцатого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell13,Ask,3*k,NULL,TPS,"Sun-LotSell13-sell(13)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell12=0;isell12<OrdersTotal();isell12++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell12, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell13-sell(13)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}


//#Четырнадцатый ордер buy
if ((CountBuy==13)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy13*k*Point))
{
CalculateBuyTP();
Print("Открытие четырнадцатого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy14,Ask,3*k,NULL,TPB,"Sun-LotBuy14-buy(14)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy13=0;ibuy13<OrdersTotal();ibuy13++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy13, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy14-buy(14)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Четырнадцатый ордер sell
if ((CountSell==13)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell13*k*Point))
{
CalculateSellTP();
Print("Открытие четырнадцатого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell14,Ask,3*k,NULL,TPS,"Sun-LotSell14-sell(14)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell13=0;isell13<OrdersTotal();isell13++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell13, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell14-sell(14)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}

//#Пятнадцатый ордер buy
if ((CountBuy==14)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy14*k*Point))
{
CalculateBuyTP();
Print("Открытие пятнадцатого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy15,Ask,3*k,NULL,TPB,"Sun-LotBuy15-buy(15)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy14=0;ibuy14<OrdersTotal();ibuy14++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy14, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy15-buy(15)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Пятнадцатый ордер sell
if ((CountSell==14)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell14*k*Point))
{
CalculateSellTP();
Print("Открытие пятнадцатого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell15,Ask,3*k,NULL,TPS,"Sun-LotSell15-sell(15)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell14=0;isell14<OrdersTotal();isell14++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell14, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell15-sell(15)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}

//#Шестнадцатый ордер buy
if ((CountBuy==15)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy15*k*Point))
{
CalculateBuyTP();
Print("Открытие шестнадцатого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy16,Ask,3*k,NULL,TPB,"Sun-LotBuy16-buy(16)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy15=0;ibuy15<OrdersTotal();ibuy15++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy15, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy16-buy(16)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Шестнадцатый ордер sell
if ((CountSell==15)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell15*k*Point))
{
CalculateSellTP();
Print("Открытие шестнадцатого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell16,Ask,3*k,NULL,TPS,"Sun-LotSell16-sell(16)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell15=0;isell15<OrdersTotal();isell15++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell15, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell16-sell(16)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}
//#Семнадцатый ордер buy
if ((CountBuy==16)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy16*k*Point))
{
CalculateBuyTP();
Print("Открытие семнадцатого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy17,Ask,3*k,NULL,TPB,"Sun-LotBuy17-buy(17)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy16=0;ibuy16<OrdersTotal();ibuy16++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy16, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy17-buy(17)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Семнадцатый ордер sell
if ((CountSell==16)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell16*k*Point))
{
CalculateSellTP();
Print("Открытие семнадцатого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell17,Ask,3*k,NULL,TPS,"Sun-LotSell17-sell(17)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell16=0;isell16<OrdersTotal();isell16++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell16, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell17-sell(17)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}
//#Восемнадцатый ордер buy
if ((CountBuy==17)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy17*k*Point))
{
CalculateBuyTP();
Print("Открытие восемнадцатого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy18,Ask,3*k,NULL,TPB,"Sun-LotBuy18-buy(18)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy17=0;ibuy17<OrdersTotal();ibuy17++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy17, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy18-buy(18)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Восемнадцатый ордер sell
if ((CountSell==17)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell17*k*Point))
{
CalculateSellTP();
Print("Открытие восемнадцатого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell18,Ask,3*k,NULL,TPS,"Sun-LotSell18-sell(18)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell17=0;isell17<OrdersTotal();isell17++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell17, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell18-sell(18)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}
//#Девятнадцатый ордер buy
if ((CountBuy==18)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy18*k*Point))
{
CalculateBuyTP();
Print("Открытие девятнадцатого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy19,Ask,3*k,NULL,TPB,"Sun-LotBuy19-buy(19)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy18=0;ibuy18<OrdersTotal();ibuy18++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy18, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy19-buy(19)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Девятнадцатый ордер sell
if ((CountSell==18)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell18*k*Point))
{
CalculateSellTP();
Print("Открытие девятнадцатого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell19,Ask,3*k,NULL,TPS,"Sun-LotSell19-sell(19)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell18=0;isell18<OrdersTotal();isell18++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell18, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell19-sell(19)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}
//#Двадцатый ордер buy
if ((CountBuy==19)&&(BuyTrade==true))
{
SearchLastBuyPrice();

if(Ask<(LastBuyPrice-LevelBuy19*k*Point))
{
CalculateBuyTP();
Print("Открытие двадцатого ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUY,LotBuy20,Ask,3*k,NULL,TPB,"Sun-LotBuy20-buy(20)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int ibuy19=0;ibuy19<OrdersTotal();ibuy19++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy19, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotBuy20-buy(20)")&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Green); }
      }      
      } 
}
}
}
}


//#Двадцатый ордер sell
if ((CountSell==19)&&(SellTrade==true))
{
SearchLastSellPrice();

if(Bid>(LastSellPrice+LevelSell19*k*Point))
{
CalculateSellTP();
Print("Открытие двадцатого ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELL,LotSell20,Ask,3*k,NULL,TPS,"Sun-LotSell20-sell(20)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()); }
        else
{
     for(int isell19=0;isell19<OrdersTotal();isell19++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell19, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderComment()!="Sun-LotSell20-sell(20)")&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      } 
}
}
}
}
}//Закрывает Limit Faulse


if((LimitsOn==true)&&((CountSell!=0)||(CountBuy!=0)))
{

SellLimitInTrade=false;BuyLimitInTrade=false;

 for(int idell=0;idell<OrdersTotal();idell++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(idell, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&((OrderType() == OP_SELLLIMIT)||(OrderType() == OP_BUYLIMIT)))
{ if(OrderType() == OP_BUYLIMIT) {BuyLimitInTrade=true;}
  if(OrderType() == OP_SELLLIMIT) {SellLimitInTrade=true;}
}
}
}

if (BuyLimitInTrade==false)
{
switch(CountBuy)                                 
     {   case 1 : for(int ibuylim=0;ibuylim<total;ibuylim++)   {
      if(OrderSelect(ibuylim, SELECT_BY_POS)==true){ 
    if (( OrderSymbol() == Symbol())&&(OrderType() == OP_BUY )) {LastBuyPrice=OrderOpenPrice();
    }}}

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy1*Point*k;
Print("Открытие второго(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy2,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy2-buy(2)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy2,Ask,3*k,NULL,NULL,"Sun-LotBuy2-buy(2)",Magic_Number,0,Blue); }
}      break;
case 2 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy2*Point*k;
Print("Открытие третьего(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy3,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy3-buy(3)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy3,Ask,3*k,NULL,NULL,"Sun-LotBuy3-buy(3)",Magic_Number,0,Blue); }
}      break;

case 3 : 
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy3*Point*k;
Print("Открытие четвертого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy4,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy4-buy(4)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_BUY,LotBuy4,Ask,3*k,NULL,NULL,"Sun-LotBuy4-buy(4)",Magic_Number,0,Blue); }
}      break;
case 4 : 
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy4*Point*k;
Print("Открытие пятого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy5,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy5-buy(5)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy5,Ask,3*k,NULL,NULL,"Sun-LotBuy5-buy(5)",Magic_Number,0,Blue); }
}      break;
case 5 : 
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy5*Point*k;
Print("Открытие шестого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy6,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy6-buy(6)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy6,Ask,3*k,NULL,NULL,"Sun-LotBuy6-buy(6)",Magic_Number,0,Blue); }
}break;
case 6 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy6*Point*k;
Print("Открытие седьмого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy7,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy7-buy(7)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy7,Ask,3*k,NULL,NULL,"Sun-LotBuy7-buy(7)",Magic_Number,0,Blue); }
}      break;
case 7 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy7*Point*k;
Print("Открытие восьмого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy8,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy8-buy(8)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy8,Ask,3*k,NULL,NULL,"Sun-LotBuy8-buy(8)",Magic_Number,0,Blue); }
}      break;
         
case 8 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy8*Point*k;
Print("Открытие девятого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy9,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy9-buy(9)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy9,Ask,3*k,NULL,NULL,"Sun-LotBuy9-buy(9)",Magic_Number,0,Blue); }
}      break;
case 9 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy9*Point*k;
Print("Открытие десятого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy10,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy10-buy(10)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy10,Ask,3*k,NULL,NULL,"Sun-LotBuy10-buy(10)",Magic_Number,0,Blue); }
}      break;     
case 10 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy10*Point*k;
Print("Открытие одинадцатого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy11,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy11-buy(11)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy11,Ask,3*k,NULL,NULL,"Sun-LotBuy11-buy(11)",Magic_Number,0,Blue); }
}      break;     

case 11 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy11*Point*k;
Print("Открытие двенадцатого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy12,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy12-buy(12)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy12,Ask,3*k,NULL,NULL,"Sun-LotBuy12-buy(12)",Magic_Number,0,Blue); }
}      break;
case 12 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy12*Point*k;
Print("Открытие тринадцатого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy13,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy13-buy(13)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy13,Ask,3*k,NULL,NULL,"Sun-LotBuy13-buy(13)",Magic_Number,0,Blue); }
}      break;
case 13 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy13*Point*k;
Print("Открытие четырнадцатого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy14,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy14-buy(14)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy14,Ask,3*k,NULL,NULL,"Sun-LotBuy14-buy(14)",Magic_Number,0,Blue); }
}      break;

case 14 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy14*Point*k;
Print("Открытие пятнадцатого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy15,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy15-buy(15)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy15,Ask,3*k,NULL,NULL,"Sun-LotBuy15-buy(15)",Magic_Number,0,Blue); }
}      break;

case 15 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy15*Point*k;
Print("Открытие шестнадцатого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy16,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy16-buy(16)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy16,Ask,3*k,NULL,NULL,"Sun-LotBuy16-buy(16)",Magic_Number,0,Blue); }
}      break;

case 16 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy16*Point*k;
Print("Открытие семнадцатого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy17,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy17-buy(17)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy17,Ask,3*k,NULL,NULL,"Sun-LotBuy17-buy(17)",Magic_Number,0,Blue); }
}      break;

case 17 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy17*Point*k;
Print("Открытие восемнадцатого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy18,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy18-buy(18)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy18,Ask,3*k,NULL,NULL,"Sun-LotBuy18-buy(18)",Magic_Number,0,Blue); }
}      break;

case 18 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy18*Point*k;
Print("Открытие девятнадцатого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy19,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy19-buy(19)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy19,Ask,3*k,NULL,NULL,"Sun-LotBuy19-buy(19)",Magic_Number,0,Blue); }
}      break;
case 19 :  
SearchLastBuyPrice();

BuyLimitPrice=0;
BuyLimitPrice=LastBuyPrice-LevelBuy19*Point*k;
Print("Открытие двадцатого(лимитного) ордера на покупку");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_BUYLIMIT,LotBuy20,BuyLimitPrice,3*k,NULL,NULL,"Sun-LotBuy20-buy(20)",Magic_Number,0,Blue) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_BUY,LotBuy19,Ask,3*k,NULL,NULL,"Sun-LotBuy20-buy(20)",Magic_Number,0,Blue); }
}      break;

     }
      
}

if (SellLimitInTrade==false)
{
 
switch(CountSell)                                 
     {     
case 1 : for(int iselllim=0;iselllim<total;iselllim++)
{
      // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(iselllim, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderType() == OP_SELL )) 
    {LastSellPrice=OrderOpenPrice();}
      } 
}
SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell1*Point*k;
Print("Открытие второго(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell2,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell2-sell(2)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_SELL,LotSell2,Bid,3*k,NULL,NULL,"Sun-LotSell2-sell(2)",Magic_Number,0,Red); }
}  break;
case 2 :{SearchLastSellPrice();
SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell2*Point*k;
Print("Открытие третьего(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell3,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell3-sell(3)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_SELL,LotSell3,Bid,3*k,NULL,NULL,"Sun-LotSell3-sell(3)",Magic_Number,0,Red); }
}   break;}
case 3 :
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell3*Point*k;
Print("Открытие четвертого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell4,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell4-sell(4)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_SELL,LotSell4,Bid,3*k,NULL,NULL,"Sun-LotSell4-sell(4)",Magic_Number,0,Red); }
}   break;
case 4 :SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell4*Point*k;
Print("Открытие пятого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell5,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell5-sell(5)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell5,Bid,3*k,NULL,NULL,"Sun-LotSell5-sell(5)",Magic_Number,0,Red);}
}   break;
case 5 :SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell5*Point*k;
Print("Открытие шестого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell6,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell6-sell(6)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка");OrderSend(Symbol(),OP_SELL,LotSell6,Bid,3*k,NULL,NULL,"Sun-LotSell6-sell(6)",Magic_Number,0,Red); }
}   break;
case 6 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell6*Point*k;
Print("Открытие седьмого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell7,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell7-sell(7)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell7,Bid,3*k,NULL,NULL,"Sun-LotSell7-sell(7)",Magic_Number,0,Red);}
}   break;

case 7 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell7*Point*k;
Print("Открытие восьмого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell8,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell8-sell(8)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell8,Bid,3*k,NULL,NULL,"Sun-LotSell8-sell(8)",Magic_Number,0,Red);}
}   break;

case 8 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell8*Point*k;
Print("Открытие девятого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell9,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell9-sell(9)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell9,Bid,3*k,NULL,NULL,"Sun-LotSell9-sell(9)",Magic_Number,0,Red);}
}   break;

case 9 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell9*Point*k;
Print("Открытие десятого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell10,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell10-sell(10)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell10,Bid,3*k,NULL,NULL,"Sun-LotSell10-sell(10)",Magic_Number,0,Red);}
}   break;


case 10 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell10*Point*k;
Print("Открытие одинадцатого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell11,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell11-sell(11)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell11,Bid,3*k,NULL,NULL,"Sun-LotSell11-sell(11)",Magic_Number,0,Red);}
}   break;

case 11 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell11*Point*k;
Print("Открытие двенадцатого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell12,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell12-sell(12)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell12,Bid,3*k,NULL,NULL,"Sun-LotSell12-sell(12)",Magic_Number,0,Red);}
}   break;

case 12 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell12*Point*k;
Print("Открытие тринадцатого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell13,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell13-sell(13)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell13,Bid,3*k,NULL,NULL,"Sun-LotSell13-sell(13)",Magic_Number,0,Red);}
}   break;

case 13 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell13*Point*k;
Print("Открытие четырнадцатого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell14,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell14-sell(14)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell14,Bid,3*k,NULL,NULL,"Sun-LotSell14-sell(14)",Magic_Number,0,Red);}
}   break;

case 14 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell14*Point*k;
Print("Открытие пятнадцатого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell15,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell15-sell(15)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell15,Bid,3*k,NULL,NULL,"Sun-LotSell15-sell(15)",Magic_Number,0,Red);}
}   break;

case 15 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell15*Point*k;
Print("Открытие шестнадцатого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell16,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell16-sell(16)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell16,Bid,3*k,NULL,NULL,"Sun-LotSell16-sell(16)",Magic_Number,0,Red);}
}   break;

case 16 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell16*Point*k;
Print("Открытие семнадцатого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell17,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell17-sell(17)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell17,Bid,3*k,NULL,NULL,"Sun-LotSell17-sell(17)",Magic_Number,0,Red);}
}   break;

case 17 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell17*Point*k;
Print("Открытие восемнадцатого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell18,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell18-sell(18)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell18,Bid,3*k,NULL,NULL,"Sun-LotSell18-sell(18)",Magic_Number,0,Red);}
}   break;
case 18 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell18*Point*k;
Print("Открытие девятнадцатого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell19,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell19-sell(19)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell19,Bid,3*k,NULL,NULL,"Sun-LotSell19-sell(19)",Magic_Number,0,Red);}
}   break;
case 19 :  
SearchLastSellPrice();

SellLimitPrice=0;
SellLimitPrice=LastSellPrice+LevelSell19*Point*k;
Print("Открытие двадцатого(лимитного) ордера на продажу");
if (IsTradeAllowed()) { if(    OrderSend(Symbol(),OP_SELLLIMIT,LotSell20,SellLimitPrice,3*k,NULL,NULL,"Sun-LotSell20-sell(20)",Magic_Number,0,Red) < 0) 
      {Alert("Ошибка открытия позиции № ", GetLastError()," Открываемся с рынка"); OrderSend(Symbol(),OP_SELL,LotSell20,Bid,3*k,NULL,NULL,"Sun-LotSell20-sell(20)",Magic_Number,0,Red);}
}   break;
     }
}
}







return(0);}

//#Рассчёт итогового профита ордеров на покупку
 double CalculateBuyTP(){
   RefreshRates();
  TPB=0;
  int CountB=1;
  double PriceB=Ask;
for(int ibuyResult=0;ibuyResult<OrdersTotal();ibuyResult++)
   {
      // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuyResult, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderType() == OP_BUY )) {PriceB=PriceB+OrderOpenPrice();CountB=CountB+1;}
      }         
   }
TPB=PriceB/CountB+TP*Point*k;   
return(TPB);
}
//#Модификация итогового профита ордеров на покупку
 double CalculateTotalBuyTP(){
TPB=0;
int CountB=0;
double PriceB=0;
for(int ibuyResult=0;ibuyResult<OrdersTotal();ibuyResult++)
   {
      // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuyResult, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderType() == OP_BUY )) {PriceB=PriceB+OrderOpenPrice();CountB=CountB+1;}
      }         
   }
   if(CountB!=0){
TPB=PriceB/CountB+TP*Point*k; 
for(int ibuy1Result=0;ibuy1Result<OrdersTotal();ibuy1Result++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuy1Result, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderType() == OP_BUY )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPB,0,Orange); }
      }      
      }}
return(TPB);
}
//#Рассчёт итогового профита ордеров на продажу
 double CalculateSellTP(){
  TPS=0;
  int CountS=1;
  double PriceS=Bid;
for(int isellResult=0;isellResult<OrdersTotal();isellResult++)
   {
      // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isellResult, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderType() == OP_SELL )) {PriceS=PriceS+OrderOpenPrice();CountS=CountS+1;}
      }         
   }
   if(CountS!=0){
TPS=PriceS/CountS-TP*Point*k; }  
return(TPS);
}
//#Модификация итогового профита ордеров на продажу
 double CalculateTotalSellTP(){
TPS=0;
int CountS=0;
double PriceS=0;
for(int isellResult=0;isellResult<OrdersTotal();isellResult++)
   {
      // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isellResult, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderType() == OP_SELL )) {PriceS=PriceS+OrderOpenPrice();CountS=CountS+1;}
      }         
   }
    if(CountS!=0){
TPS=PriceS/CountS-TP*Point*k; 
for(int isell1Result=0;isell1Result<OrdersTotal();isell1Result++)
      { // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isell1Result, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderType() == OP_SELL )) {
   RefreshRates();
   OrderModify(OrderTicket(),OrderOpenPrice(),OrderStopLoss(),TPS,0,Orange); }
      }      
      }}
return(TPS);
}


//#Поиск последнего ордера на покупку
double SearchLastBuyPrice()
{
LastBuyPrice=0;  
for(int ibuySearch=0;ibuySearch<OrdersTotal();ibuySearch++)
   {
       // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(ibuySearch, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderType() == OP_BUY )) 
{
if(LastBuyPrice==0){LastBuyPrice=OrderOpenPrice();}    
if(LastBuyPrice>OrderOpenPrice()){LastBuyPrice=OrderOpenPrice();}             
}
      }         
   }
return(LastBuyPrice);
}

//#Поиск последнего ордера на продажу
double SearchLastSellPrice()
{
LastSellPrice=0;  
for(int isellSearch=0;isellSearch<OrdersTotal();isellSearch++)
   {
       // результат выбора проверки, так как ордер может быть закрыт или удален в это время!
      if(OrderSelect(isellSearch, SELECT_BY_POS)==true)
      { 
    if (( OrderSymbol() == Symbol())&&(OrderType() == OP_SELL )) 
{
if(LastSellPrice==0){LastSellPrice=OrderOpenPrice();}    
if(LastSellPrice<OrderOpenPrice()){LastSellPrice=OrderOpenPrice();}             
}
      }         
   }
return(LastSellPrice);
}

double OrdersDel()
{for (int iDel1=OrdersTotal()-1; iDel1>=0; iDel1--)
   {
      if (!OrderSelect(iDel1,SELECT_BY_POS,MODE_TRADES)) break;
            if (((OrderType()==OP_BUYLIMIT  )||(OrderType()==OP_SELLLIMIT  ))&&(OrderMagicNumber() == Magic_Number ))    if (IsTradeAllowed()) { if (OrderDelete(OrderTicket())<0) 
            { 
        Alert("Ошибка удаления ордера № ", GetLastError()); 
      }  
            }
} return(Magic_Number);}

double BuyLimDel()
{for (int iDel1=OrdersTotal()-1; iDel1>=0; iDel1--)
   {
      if (!OrderSelect(iDel1,SELECT_BY_POS,MODE_TRADES)) break;
            if ((OrderType()==OP_BUYLIMIT)&&(OrderMagicNumber() == Magic_Number ))    if (IsTradeAllowed()) { if (OrderDelete(OrderTicket())<0) 
            { 
        Alert("Ошибка удаления ордера № ", GetLastError()); 
      }  
            }
} return(Magic_Number);}

double SellLimDel()
{for (int iDel2=OrdersTotal()-1; iDel2>=0; iDel2--)
   {
      if (!OrderSelect(iDel2,SELECT_BY_POS,MODE_TRADES)) break;
            if ((OrderType()==OP_SELLLIMIT)&&(OrderMagicNumber() == Magic_Number ))    if (IsTradeAllowed()) { if (OrderDelete(OrderTicket())<0) 
            { 
        Alert("Ошибка удаления ордера № ", GetLastError()); 
      }  
            }
} return(Magic_Number);}

bool isNewBar()
  {
  static datetime BarTime;  
   bool res=false;
    
   if (BarTime!=Time[0]) 
      {
         BarTime=Time[0];  
         res=true;
      } 
   return(res);
  }
  
//---- Возвращает количество ордеров указанного типа ордеров ----//
int Orders_Total_by_type(int type, int mn, string sym)
{
   int num_orders=0;
   for(int i= OrdersTotal()-1;i>=0;i--)
   {
      OrderSelect(i,SELECT_BY_POS,MODE_TRADES);
      if(OrderMagicNumber() == mn && type == OrderType() && sym==OrderSymbol())
         num_orders++;
   }
   return(num_orders);
}
