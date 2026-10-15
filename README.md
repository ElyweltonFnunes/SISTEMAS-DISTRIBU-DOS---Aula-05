# SISTEMAS-DISTRIBU-DOS---Aula-05
Concorrência e Sincronização

import threading
import time

saldo = 1000

def sacar(valor):
    global saldo

    saldo_atual = saldo
    time.sleep(0.01)
    saldo = saldo_atual - valor

threads = []

for i in range(10):
    t = threading.Thread(target=sacar, args=(50,))
    threads.append(t)
    t.start()
    
for t in threads:
    t.join()

print("Saldo esperado: 500")
print("Saldo obtido:", saldo)

• As threads compartilharam a variável saldo.
R = Sim, As threads compartilham a variável global saldo.

• Mais de uma thread conseguiu ler o mesmo valor antes de outra terminar a atualização.
R = SIM.

• Depois, diferentes threads gravaram resultados calculados a partir de valores antigos.
R = Sim, Diferentes threads gravaram resultados calculados a partir de valores antigos.



