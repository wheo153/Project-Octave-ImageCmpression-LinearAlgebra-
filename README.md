# Project-Octave-ImageCmpression-LinearAlgebra-
Image Compression by using the Singular value decomposition (Octave)
%% Project2 Wonju Heo
% Image Compression 
% i. importing an image
A1=imread('Lion.jpg');
Image1 = im2double(A1);     // Converting image to Double
[U1,S1,V1] = svd(Image1);   // Assign tha variables U1, S1, V1 by using svd() function

A2=imread('Flower.jpg');
Image2 = im2double(A2);
[U2,S2,V2] = svd(Image2);

% ii.
% performing 
s1_5= S1;                   //S1 is n x p matrix, s1_5 is a 5x5 matrix having zeros when k > 5
s1_5(6:end, :) = 0;         //Making all values as Zero except less than 6. (5x5 matrix remained)
s1_5(:, 6:end) = 0;         //Making all values as Zero except less than 6. (5x5 matrix remained)

A1_5 = U1*s1_5*V1';         //A1_5 has the values of compressed image (K=5)

s1_15= S1;
s1_15(11:end, :) = 0;
s1_15(:, 11:end) = 0;

A1_15 = U1*s1_15*V1';

s1_50 = S1;
s1_50(31:end, :) = 0;
s1_50(:, 31:end) = 0;

A1_50 = U1*s1_50*V1';

s1 = S1;
s1(151:end, :) = 0;
s1(:, 151:end) = 0;

A1 = U1*s1*V1';

figure(1)
  subplot(2,2,1)  
  imshow(A1_5);                     //Printing the image of the Compress matrix A1_5
  title ('k=5',"fontsize",20);
  subplot(2,2,2)
  imshow(A1_15);
  title ('k=15',"fontsize",20);
  subplot(2,2,3)
  imshow(A1_50);
  title ('k=50',"fontsize",20);
  subplot(2,2,4)
  imshow(A1);
  title ('Original',"fontsize",20);

s2_5= S2;
s2_5(6:end, :) = 0;
s2_5(:, 6:end) = 0;

A2_5 = U2*s2_5*V2';

s2_15= S2;
s2_15(11:end, :) = 0;
s2_15(:, 11:end) = 0;

A2_15 = U2*s2_15*V2';

s2_50 = S2;
s2_50(31:end, :) = 0;
s2_50(:, 31:end) = 0;

A2_50 = U2*s2_50*V2';

s2 = S2;
s2(151:end, :) = 0;
s2(:, 151:end) = 0;

A2 = U2*s2*V2';

figure(2)
  subplot(2,2,1)
  imshow(A2_5);
  title ('k=5',"fontsize",20);
  subplot(2,2,2)
  imshow(A2_15);
  title ('k=15',"fontsize",20);
  subplot(2,2,3)
  imshow(A2_50);
  title ('k=50',"fontsize",20);
  subplot(2,2,4)
  imshow(A2);
  title ('Original',"fontsize",20);
% iii.
Singularlog1 = diag(S1);
Singularlog2 = diag(S2);
figure(3)
subplot(2,1,1)
plot(Singularlog1);
title ('The singular values of A vs. k for Lion image',"fontsize",20);
xlabel("k","fontsize",16);
ylabel("The singular values of A","fontsize",16);
subplot(2,1,2)
plot(Singularlog2);
title ('The singular values of A vs. k for Flower image',"fontsize",20);
xlabel("k","fontsize",16);
ylabel("The singular values of A","fontsize",16);

% iv. 
E = 0.002;
Max1 = max(Singularlog1);
Ref1 = Singularlog1(1);

k1 = 1;
L1 = length(Singularlog1);
for i = 1 : L1
  Ref1 = Singularlog1(i);
  if Ref1 > Max1*E
    k1 = k1 +1;
   endif 
endfor

s_k1 = S1;
s_k1(k1+1:end, :) = 0;
s_k1(:, k1+1:end) = 0;
A_k1 = U1*s_k1*V1';

Max2 = max(Singularlog2);
Ref2 = Singularlog2(1);
k2 = 1;
L2 = length(Singularlog2);
for i = 1 : L2 
  Ref2 = Singularlog2(i);
  if Ref2 > Max2*E
    k2 = k2 +1;
   endif 
endfor

s_k2 = S2;
s_k2(k2+1:end, :) = 0;
s_k2(:, k2+1:end) = 0;
A_k2 = U2*s_k2*V2';

figure(4)
subplot(1,2,1)
imshow(A_k1);
title(['Compressed Lion image';
'k is ' num2str(k1) ' when epsilon is ' num2str(E)],"fontsize",16)
subplot(1,2,2)
imshow(A_k2);
title(['Compressed Flower image';
'k is ' num2str(k2) ' when epsilon is ' num2str(E)],"fontsize",16)
