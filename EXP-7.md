# AIM:
To implement error control coding schemes with linear block codes using MATLAB.

# SOFTWARE REQUIRED: 
  MATLAB

# PROGRAM:
# ERROR CODING
# ENCODING:
```
clc;
clear;
close all;

msg = [
    1 0 0 1
    1 0 1 0
    1 0 1 1
];

% Parity matrix for a systematic (7,4) cyclic/Hamming code
P = [
    1 1 0
    1 0 1
    0 1 1
    1 1 1
];

% Generator matrix G = [I4 P]
G = [eye(4), P];

% Binary encoding
code = mod(msg * G, 2);

disp('msg =');
disp(msg);

disp('code =');
disp(code);
```
# ENCODING OUTPUT:
<img width="473" height="322" alt="image" src="https://github.com/user-attachments/assets/32dee773-48ef-47ea-a1c0-b01f4ff15cf3" />

# DECODING PROGRAM:
```
clc;
clear;
close all;

q = 3;
n = 2^q - 1;
k = n - q;

% Parity-check matrix for the (7,4) Hamming code
parmat = [
    1 0 0 0 1 1 1
    0 1 0 1 1 1 0
    0 0 1 1 0 1 1
];

% Received codeword
recd = [1 0 1 1 1 1 0]; 

% Calculate the syndrome
syndrome = mod(recd * parmat', 2);

% Convert left-MSB binary syndrome to decimal
syndrome_de = syndrome * (2.^(q-1:-1:0))';

fprintf('syndrome = %d (decimal)  ', syndrome_de);
fprintf('%d ', syndrome);
fprintf('(binary)\n\n');

% Locate the erroneous bit
error_position = find(all(parmat == syndrome', 1), 1);

% Create correction vector
corrvect = zeros(1, n);

if ~isempty(error_position)
    corrvect(error_position) = 1;
end

% Correct the received codeword
correctedcode = mod(recd + corrvect, 2);

disp('parmat =');
disp(parmat);

disp('corrvect =');
disp(corrvect);

disp('correctedcode =');
disp(correctedcode);
```
# DECODING OUTPUT:
<img width="415" height="267" alt="image" src="https://github.com/user-attachments/assets/ce1e6214-cb04-444d-be85-f347f8dd1627" />

# RESULT:
Thus encoding and decoding of block codes are performed using MATLAB.

