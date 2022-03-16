# Matlab-m-file to calculate average fluorescent intenity from confocal images
clear all;clc
close all;

a=imread('Untitled15_c1.tif');% Confocal independt unit8 images, Cy5-BSA leakage 
b=imread('Untitled15_c3.tif');% Confocal independt unit8 images, vessel markers

a_cal=im2double(a); % transformation from unit8 to double type;
a_cal_1=a_cal(:,:,1); % layer containing RGB information

b_cal=im2double(b); % transformation from unit8 to double type;
b_cal_1=b_cal(:,:,2); % layer containing RGB information

[a1 a2]=size(a_cal_1); 
[b1 b2]=size(b_cal_1);

aa=zeros(a1,a2);
bb=zeros(b1,b2);
t0=0; % number of excluded pixls for further area calculation 
sum=0; % number of fluorescent pixls for further average_intensity calculation 

for i=1:b1
    for j=1:b2
        if b_cal_1(i,j)>0.15
            aa(i,j)==0;
            t0=t0+1;
        else
            aa(i,j)=a_cal_1(i,j);
        end
    end
end
imshow(aa);

for k=1:b1
    for m=1:b2
        sum=sum+aa(k,m);
    end
end

average_intensity=sum/(a1*a2-t0); 
