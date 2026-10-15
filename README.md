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


import threading
import time

saldo = 1000
lock = threading.Lock()

def sacar(valor):
    global saldo

    with lock:
        saldo_atual = saldo
        time.sleep(0.01)
        saldo = saldo_atual - valor

threads = []


print("Saldo esperado: 500")
print("Saldo obtido:", saldo)

for i in range(10):
    t = threading.Thread(target=sacar, args=(50,))
    threads.append(t)
    t.start()

for t in threads:
    t.join()

import threading
import time

estoque = 5
lock = threading.Lock()

def comprar(cliente):
    global estoque

    with lock:
        if estoque > 0:
            print(cliente, "encontrou", estoque, "unidade(s)")
            time.sleep(0.5)
            estoque -= 1
            print(cliente, "comprou. Restam:", estoque)
        else:
            print(cliente, "não conseguiu comprar: estoque esgotado")

clientes = []

for i in range(1, 9):
    t = threading.Thread(target=comprar, args=(f"Cliente {i}",))
    clientes.append(t)
    t.start()

for t in clientes:
    t.join()

print("Estoque final:", estoque)



• Tivemos uma condição de corrida.
R = Sim, Tivemos uma condição de corrida (race condition).
Isso aconteceu porque várias threads acessaram e modificaram a variável compartilhada saldo simultaneamente, sem sincronização.

