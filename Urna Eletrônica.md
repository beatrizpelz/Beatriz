const int BOTAO1=2, BOTAO2=3, BOTAO3=4, BOTAO4=5, BOTAO5=6, BOTAO6=7, BOTAO7=8, BOTAO8=9, BOTAO9=10, CONFIRMAG=11, CONFIRMAP=12;
#define G 6
#define P 9
#define TAM 50
int matriz[G][9]={0}, g=0, p=0, i=0, j=0, k=0, a=0, c=0, d=0, e=0, quantidade=0, governador[G]={0}, presidente[P]={0};
float b=0;

typedef enum {inexistente, Alvaro_Dias, Cabo_Daciolo, Ciro_Gomes, Eymael, Fernando_Haddad, Boulos, Jair_Bolsonaro, Joao_Amoedo, Marina_Silva }NumeroP;
typedef enum {inexistente2, Cida_Borghetti, Dr_Rosinha, Joao_Arruda, Ogier_Buchi, Ratinho_Jr, Prof_Piva }NumeroG;

typedef struct {
    char candidatoP[TAM];
    int votosP;
}Presidente;

typedef struct {
    char candidatoG[TAM];
    int votosG;
}Governador;

void somaPG(int g, int p, int matriz[G][9]){
    switch(p){
        case Alvaro_Dias:
            matriz[g-1][0]++;
        break;
        case Cabo_Daciolo:
            matriz[g-1][1]++;
        break;
        case Ciro_Gomes:
            matriz[g-1][2]++;
        break;
        case Eymael:
            matriz[g-1][3]++;
        break;
        case Fernando_Haddad:
            matriz[g-1][4]++;
        break;
        case Boulos:
            matriz[g-1][5]++;
        break;
        case Jair_Bolsonaro:
            matriz[g-1][6]++;
        break;
        case Joao_Amoedo:
            matriz[g-1][7]++;
        break;
        case Marina_Silva:
            matriz[g-1][8]++;
        break;
        default:
        break;
    }
}

void resultadosGovernador(int matriz[G][P]){
    Governador vetorG[G]={{"Cida Borghetti", 0},
                            {"Dr Rosinha", 0},
                            {"Joao Amoedo", 0},
                            {"Ogier Buchi", 0},
                            {"Ratinho Jr", 0},
                            {"Prof Piva", 0} }, auxG;
    NumeroG y;

    for(i=0;i<G;i++)
        for(j=0;j<P;j++)
            governador[i]+= matriz[i][j];

        for(i=0;i<G;i++)
        vetorG[i].votosG=governador[i];

    for(i=0;i<G-1;i++)
        for(j=0;j<G-1;j++)
            if(vetorG[j].votosG<vetorG[j+1].votosG){
                auxG = vetorG[j];
                vetorG[j] = vetorG[j+1];
                vetorG[j+1] = auxG;
            }

    for(i=1;i<G;i++){
      if(vetorG[0].votosG==vetorG[i].votosG){
        Serial.println("Empate entre: ");
        Serial.println(vetorG[0].candidatoG);
        Serial.println(vetorG[i].candidatoG);
        d=1;
        break;
      }
    }

    if(d!=1){
    Serial.println("\nO governador eleito foi: ");
    Serial.println(vetorG[0].candidatoG);
    }
    
    Serial.println("\nAs porcentagens de votos para cada candidado a governador são: ");
    for(i=0;i<G;i++){
      b=((vetorG[i].votosG*100)/(quantidade-1));
      Serial.println(vetorG[i].candidatoG);
      Serial.println(b);
    }  
}

void resultadosPresidente(int matriz[G][P]){
   Presidente vetorP[P]={{"Alvaro Dias", 0},
                            {"Cabo Daciolo", 0},
                            {"Ciro Gomes", 0},
                            {"Eymael", 0},
                            {"Fernando Haddad", 0},
                            {"Boulos", 0},
                            {"Jair Bolsonaro", 0},
                            {"Joao Amoedo", 0},
                            {"Marina Silva", 0} }, auxP;
   
    NumeroP x;
   
    for(i=0;i<P;i++)
        for(j=0;j<G;j++)
            presidente[i]+=matriz[j][i];

    for(i=0;i<P;i++)
        vetorP[i].votosP=presidente[i];
    

    for(i=0;i<P-1;i++)
        for(j=0;j<P-1;j++)
            if(vetorP[j].votosP<vetorP[j+1].votosP){
                auxP = vetorP[j];
                vetorP[j] = vetorP[j+1];
                vetorP[j+1] = auxP;
            }

    for(i=1;i<P;i++){
      if(vetorP[0].votosP==vetorP[i].votosP){
        Serial.println("\nEmpate entre: ");
        Serial.println(vetorP[0].candidatoP);
        Serial.println(vetorP[i].candidatoP);
        e=1;
        break;
      }
    }

    if(e!=1){
    Serial.println("\nO presidente eleito foi: ");
    Serial.println(vetorP[0].candidatoP);
    }
    
    Serial.println("\nAs porcentagens de votos para cada candidado a presidencia são: ");
    for(i=0;i<P;i++){
      b=((vetorP[i].votosP*100)/(quantidade-1));
      Serial.println(vetorP[i].candidatoP);
      Serial.println(b);
    }   
}



void eleicao(){
  do{
  Serial.println("Digite o Governador: \n");
  i=0;
  while(i!=11){
    if(digitalRead(BOTAO1)==LOW)
      g=1;
    if(digitalRead(BOTAO2)==LOW)
      g=2;
    if(digitalRead(BOTAO3)==LOW)
      g=3;
    if(digitalRead(BOTAO4)==LOW)
      g=4;
    if(digitalRead(BOTAO5)==LOW)
      g=5;
    if(digitalRead(BOTAO6)==LOW)
      g=6;
    if(digitalRead(BOTAO7)==LOW)
      g=7;
    if(digitalRead(BOTAO8)==LOW)
      g=8;
    if(digitalRead(BOTAO9)==LOW)
      g=9;
    if(digitalRead(CONFIRMAG)==LOW)
      i=11;
  }
  //Serial.println(g);
  j=0;
  Serial.println("Digite o Presidente: \n");
  while(j!=12){
    if(digitalRead(BOTAO1)==LOW)
      p=1;
    if(digitalRead(BOTAO2)==LOW)
      p=2;
    if(digitalRead(BOTAO3)==LOW)
      p=3;
    if(digitalRead(BOTAO4)==LOW)
      p=4;
    if(digitalRead(BOTAO5)==LOW)
      p=5;
    if(digitalRead(BOTAO6)==LOW)
      p=6;
    if(digitalRead(BOTAO7)==LOW)
      p=7;
    if(digitalRead(BOTAO8)==LOW)
      p=8;
    if(digitalRead(BOTAO9)==LOW)
      p=9;
    if(digitalRead(CONFIRMAP)==LOW)
      j=12;          
  }
  //Serial.println(p);
  switch(g){
        case Cida_Borghetti:
            somaPG(g, p, matriz);
        break;
        case Dr_Rosinha:
            somaPG(g, p, matriz);
        break;
        case Joao_Arruda:
            somaPG(g, p, matriz);
        break;
        case Ogier_Buchi:
            somaPG(g, p, matriz);
        break;
        case Ratinho_Jr:
            somaPG(g, p, matriz);
        break;
        case Prof_Piva:
            somaPG(g, p, matriz);
        break;
        default:
        break;
    }  
    quantidade++;
  }while(g!=9 );
  }

void setup() {
  Serial.begin(9600);
  pinMode(BOTAO1, INPUT_PULLUP);
  pinMode(BOTAO2, INPUT_PULLUP);
  pinMode(BOTAO3, INPUT_PULLUP);
  pinMode(BOTAO4, INPUT_PULLUP);
  pinMode(BOTAO5, INPUT_PULLUP);
  pinMode(BOTAO6, INPUT_PULLUP);
  pinMode(BOTAO7, INPUT_PULLUP);
  pinMode(BOTAO8, INPUT_PULLUP);
  pinMode(BOTAO9, INPUT_PULLUP);
  pinMode(CONFIRMAP, INPUT_PULLUP);
  pinMode(CONFIRMAG, INPUT_PULLUP);
}

void loop() {
  while(a!=1){
    eleicao();
    a++;
  }  
  while(c!=1){
    resultadosGovernador(matriz);
    c++;
  }
  while(k!=1){
    resultadosPresidente(matriz);
    k++;
  }    
}
