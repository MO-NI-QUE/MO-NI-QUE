[ ]  class Vertice:

  def __init__(self, rotulo, distancia_objetivo):
    self.rotulo = rotulo
    self.visitado = False
    self.distancia_objetivo = distancia_objetivo
    self.adjacentes = []

  def adiciona_adjacente(self, adjacente):
    self.adjacentes.append(adjacente)

  def mostra_adjacentes(self):
    for i in self.adjacentes:
      print(i.vertice.rotulo, i.custo)
      
 [ ]  class Adjacente:
  def __init__(self, vertice, custo):
    self.vertice = vertice
    self.custo = custo
    #atributo novo para o algoritmo:
    self.distancia_aestrela = vertice.distancia_objetivo + self.custo
    
    class Grafo:

  arad = Vertice('Arad', 366)
  zerind = Vertice('Zerind', 374)
  oradea = Vertice('Oradea', 380)
  sibiu = Vertice('Sibiu', 253)
  timisoara = Vertice('Timisoara', 329)
  lugoj = Vertice('Lugoj', 244)
  mehadia = Vertice('Mehadia', 241)
  dobreta = Vertice('Dobreta', 242)
  craiova = Vertice('Craiova', 160)
  rimnicu = Vertice('Rimnicu', 193)
  fagaras = Vertice('Fagaras', 178)
  pitesti = Vertice('Pitesti', 98)
  bucharest = Vertice('Bucharest', 0)
  giurgiu = Vertice('Giurgiu', 77)

  arad.adiciona_adjacente(Adjacente(zerind, 75))
  arad.adiciona_adjacente(Adjacente(sibiu, 140))
  arad.adiciona_adjacente(Adjacente(timisoara, 118))

  zerind.adiciona_adjacente(Adjacente(arad, 75))
  zerind.adiciona_adjacente(Adjacente(oradea, 71))

  oradea.adiciona_adjacente(Adjacente(zerind, 71))
  oradea.adiciona_adjacente(Adjacente(sibiu, 151))

  sibiu.adiciona_adjacente(Adjacente(oradea, 151))
  sibiu.adiciona_adjacente(Adjacente(arad, 140))
  sibiu.adiciona_adjacente(Adjacente(fagaras, 99))
  sibiu.adiciona_adjacente(Adjacente(rimnicu, 80))

  timisoara.adiciona_adjacente(Adjacente(arad, 118))
  timisoara.adiciona_adjacente(Adjacente(lugoj, 111))

  lugoj.adiciona_adjacente(Adjacente(timisoara, 111))
  lugoj.adiciona_adjacente(Adjacente(mehadia, 70))

  mehadia.adiciona_adjacente(Adjacente(lugoj, 70))
  mehadia.adiciona_adjacente(Adjacente(dobreta, 75))

  dobreta.adiciona_adjacente(Adjacente(mehadia, 75))
  dobreta.adiciona_adjacente(Adjacente(craiova, 120))

  craiova.adiciona_adjacente(Adjacente(dobreta, 120))
  craiova.adiciona_adjacente(Adjacente(pitesti, 138))
  craiova.adiciona_adjacente(Adjacente(rimnicu, 146))

  rimnicu.adiciona_adjacente(Adjacente(craiova, 146))
  rimnicu.adiciona_adjacente(Adjacente(sibiu, 80))
  rimnicu.adiciona_adjacente(Adjacente(pitesti, 97))

  fagaras.adiciona_adjacente(Adjacente(sibiu, 99))
  fagaras.adiciona_adjacente(Adjacente(bucharest, 211))

  pitesti.adiciona_adjacente(Adjacente(rimnicu, 97))
  pitesti.adiciona_adjacente(Adjacente(craiova, 138))
  pitesti.adiciona_adjacente(Adjacente(bucharest, 101))

  bucharest.adiciona_adjacente(Adjacente(fagaras, 211))
  bucharest.adiciona_adjacente(Adjacente(pitesti, 101))
  bucharest.adiciona_adjacente(Adjacente(giurgiu, 90))
  
  [ ] grafo = Grafo()
  
 [ ] class BuscaAEstrela:
  def __init__(self, objetivo):
    self.objetivo = objetivo
    self.encontrado = False
  
  def buscar(self, atual):
    print("---------------")
    print(f"Cidade Atual: {atual.rotulo}")

    if atual == self.objetivo:
      self.encontrado = True
      print("Objetivo encontrado! :D")
    else:
      vetor_ordenado = VetorOrdenado(len(atual.adjacentes))
      for adjacente in atual.adjacentes:
        if adjacente.vertice.visitado == False:
          adjacente.vertice.visitado = True
          vetor_ordenado.insere(adjacente)
      vetor_ordenado.imprime()

      if vetor_ordenado.valores[0] != None:
        self.buscar(vetor_ordenado.valores[0].vertice)
        
        busca_aestrela = BuscaAEstrela(grafo.bucharest)
busca_aestrela.buscar(grafo.arad)

Cidade Atual: Arad
0  -  Sibiu  - Custo: 140  - Distância em linha reta: 253  - Soma: 393
1  -  Timisoara  - Custo: 118  - Distância em linha reta: 329  - Soma: 447
---------------
Cidade Atual: Sibiu
0  -  Rimnicu  - Custo: 80  - Distância em linha reta: 193  - Soma: 273
1  -  Fagaras  - Custo: 99  - Distância em linha reta: 178  - Soma: 277
2  -  Arad  - Custo: 140  - Distância em linha reta: 366  - Soma: 506
3  -  Oradea  - Custo: 151  - Distância em linha reta: 380  - Soma: 531
---------------
Cidade Atual: Rimnicu
0  -  Pitesti  - Custo: 97  - Distância em linha reta: 98  - Soma: 195
1  -  Craiova  - Custo: 146  - Distância em linha reta: 160  - Soma: 306
---------------
Cidade Atual: Pitesti
0  -  Bucharest  - Custo: 101  - Distância em linha reta: 0  - Soma: 101
---------------
Cidade Atual: Bucharest
Objetivo encontrado! :D
  
  
