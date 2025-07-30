# Joc-2D-pe-FPGA-cu-Controler-VGA-1080p-in-Verilog

Joc 2D pe FPGA cu Controler VGA 1080p în Verilog

📝 Descriere Generală
Acest proiect este o implementare în Verilog a unui joc 2D simplu, conceput să ruleze pe o placă de dezvoltare FPGA (Digilent Basys 3). Proiectul generează un semnal video VGA cu o rezoluție de 1920x1080 (1080p).

Jocul constă în controlarea unui triunghi roșu pe ecran, cu scopul de a evita obstacole albastre care se deplasează orizontal. La detectarea unei coliziuni, jocul se resetează la starea inițială.

🛠️ Hardware și Software
Hardware Necesar
O placă de dezvoltare 

Digilent Basys 3 

Un monitor cu intrare VGA

Un cablu VGA

Software Necesar
Xilinx Vivado Design Suite: Proiectul utilizează un fișier de constrângeri (.xdc), specific acestui software.

📁 Structura Proiectului
Proiectul este format din următoarele module Verilog și un fișier de constrângeri:

1. vga_top.v
Acesta este modulul de top care integrează toate celelalte componente ale sistemului.



Instanțiază un wrapper pentru ceas (

design_1_wrapper) pentru a genera frecvența necesară semnalului VGA.

Instanțiază controlerul de temporizare VGA (

vga_1920X1080).

Instanțiază modulul cu logica jocului (

vga_deplasare).

Conectează intrările (ceas, reset, butoane) și ieșirile (semnalele VGA RGB, Hsync, Vsync) la pinii externi ai FPGA-ului.



2. vga_1920X1080.v
Acest modul este responsabil pentru generarea semnalelor de temporizare VGA, conform standardului de 1920x1080 @ 60Hz.

Utilizează contoare orizontale (

h_counter) și verticale (v_counter) pentru a urmări poziția curentă a fasciculului de electroni pe ecran.


Generează semnalele de sincronizare 

h_sync și v_sync.

Produce un semnal 

display_surface care indică zona vizibilă a ecranului.

3. vga_deplasare.v
Acesta este modulul care conține logica jocului.


Renderizare Obiecte: Desenează un triunghi roșu (jucătorul) și obstacole albastre pe ecran.


Control Utilizator: Preia intrările de la butoanele btnU, btnD, btnL, btnR pentru a deplasa triunghiul.


Mișcare Obstacole: Implementează logica pentru deplasarea orizontală, automată a obstacolelor.


Detecție Coliziuni: Verifică dacă există o suprapunere între coordonatele triunghiului și cele ale obstacolelor. La coliziune, resetează poziția jucătorului și a obstacolelor.



4. Basys3_Master.xdc
Acesta este fișierul de constrângeri care mapează porturile definite în vga_top.v la pinii fizici ai plăcii Basys 3.


Ceas principal: Pin W5 

Butoane:


rst: Pin U18 


btnU: Pin T18 


btnD: Pin U17 


btnL: Pin W19 


btnR: Pin T17 

Ieșiri VGA:


Hsync: Pin P19 


Vsync: Pin R19 


vgaRed[3:0]: Pini N19, J19, H19, G19 


vgaGreen[3:0]: Pini D17, G17, H17, J17 


vgaBlue[3:0]: Pini J18, K18, L18, N18 
![img1](https://github.com/user-attachments/assets/233a3ab8-4a86-49b9-a720-41fffcbcf739)  
![img2](https://github.com/user-attachments/assets/aad6efb3-906a-4e43-96c3-2119b61978b0)
