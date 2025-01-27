clc 
clear all
close all
P=zeros(1,28);
T=zeros(1,28);
N=122:(-10/28):112;
P(1)=300;
T(1)=300;
Z=zeros(1,29);
Z(29)=28;
M=zeros(1,29);
M(29)=3.136;
a=1;
 veri1=readtable('refprop_nitrogen_yeni (2).csv');
 veri2=table2array(veri1);
 [x,y]=size(veri2);
 for i=1:x
     ET(i)=veri2(i,1);
     EP(i)=veri2(i,2);
     ER(i)=veri2(i,3);
 end
 ED=zeros(1,28);
 k=1;
 while a<29
     T(a+1)=(((T(a)^(5/2))*N(a+1))/N(a))^(2/5);
     P(a+1)=(P(a)*N(a+1)*T(a+1))/(N(a)*T(a));
     Z(a)=a-1;
     M(a)=(N(a)*28)/1000;
     X=find(EP==(round(P(a))/10));
     Y=find(ET==(round(T(a))));
     L=intersect(X,Y);
     ED(a)=EP(L(1)); 
     a=a+1;
 end
plot(Z(1:end-1),ED,o)
xlabel('zaman')
ylabel('yoğunluk')
title('zamanla yoğunluk değişimi')
figure(2)
plot(Z,T,o)
xlabel('zaman')
ylabel('sıcaklık')
title('sıcaklık zaman')
figure (3)
plot(Z,P,o)
xlabel('zaman')
ylabel('basınç')
title('basınç zaman')
