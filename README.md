import os

arquivo_perfil = 'perfil.txt'

def verificar_perfil(nome):
    if not os.path.exists(arquivo_perfil):
        return None
    with open(arquivo_perfil, 'r') as arquivo:
        for linha in arquivo:
            dados = linha.strip().split(';')
            if dados[0] == nome:
                return dados
    return None

def criar_perfil():
    nome = input("Digite seu nome: ")
    altura = float(input("Digite sua altura (em cm): "))
    peso = float(input("Digite seu peso (em kg): "))
    genero = input("Digite seu gênero: ")
    sexo = input("Digite seu sexo: ")
    
    # Abrir e fechar o arquivo para escrita
    with open(arquivo_perfil, 'a') as arquivo:
        arquivo.write(f"{nome};{altura};{peso};{genero};{sexo}\n")
    print("\nPerfil criado com sucesso!\n")

def editar_perfil(nome):
    novo_nome = input("Digite o novo nome: ")
    altura = float(input("Digite a nova altura (em cm): "))
    peso = float(input("Digite o novo peso (em kg): "))
    genero = input("Digite o novo gênero: ")
    sexo = input("Digite o novo sexo: ")
    
   # Leitura das linhas do arquivo
    arquivo = open(arquivo_perfil, 'r')
    linhas = arquivo.readlines()
    arquivo.close()
    
    # Reescrita do arquivo com os dados atualizados
    arquivo = open(arquivo_perfil, 'w')
    for linha in linhas:
        if linha.startswith(nome):
            arquivo.write(f"{novo_nome};{altura};{peso};{genero};{sexo}\n")
        else:
            arquivo.write(linha)
    arquivo.close()
    
    print("\nPerfil atualizado com sucesso!\n")

def abrir_perfil():
    nome = input("Digite seu nome: ")
    perfil = verificar_perfil(nome)
    
    if perfil:
        print("\n--- Perfil Encontrado ---")
        print(f"Nome: {perfil[0]}")
        print(f"Altura: {perfil[1]} cm")
        print(f"Peso: {perfil[2]} kg")
        print(f"Gênero: {perfil[3]}")
        print(f"Sexo: {perfil[4]}")
        print("\nDigite 1 para editar ou 2 para sair.")
        
        opcao = input("Escolha: ")
        if opcao == '1':
            editar_perfil(nome)
        elif opcao == '2':
            print("\nSaindo da aba de perfil...\n")
    else:
        print("\nPerfil não encontrado. Vamos criar um novo.")
        criar_perfil()

# Execução
abrir_perfil()
