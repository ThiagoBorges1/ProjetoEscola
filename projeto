from descricoes import *
import random
import time

def mostrar_turmas(): 
    print(f'{"="*25}\n|| Turmas: \n||{"="*23}')
    for tur in lista_turmas:
        print(f'|| ({lista_turmas.index(tur)+1}) - Turma: {tur.nome} - {tur.curso} - sE: {tur.segmentoEnsino} - {tur.anoEscolar} - Alunos : {len(tur.alunos)}')
        print(f'||  Diciplinas da turma: ') if len(tur.disciplinas) > 0 else False
        for d in tur.disciplinas: 
            print(f'||  Número: {tur.disciplinas.index(d)+ 1} Id: {d.id}')
        print('||'+'='*5)if len(tur.disciplinas) > 0 else False
    print(f'|| ({len(lista_turmas)+1}) - Sair')
    print(f'||{"="*23}')
    try:
        turma_escolhida = lista_turmas[int(input('|| Digite o número da turma: ')) - 1]
    except:
        return 
    return turma_escolhida

def mostrar_disciplinas(): 
    if len(lista_disciplinas) == 0:
        return None
    print(f'{"="*25}\n|| Disciplinas: \n{"="*25}')
    
    for disc in lista_disciplinas:
        if isinstance(disc.professor, Professor):
            print(f'|| ({lista_disciplinas.index(disc)+1}) - Id: {disc.id}| Descrição: {disc.descricao}| sE: {disc.segmentoEnsino}| professor: {disc.professor.nome} {disc.professor.sobrenome}')
        elif disc.professor == None:
            print(f'|| ({lista_disciplinas.index(disc)+1}) - Id: {disc.id}| Descrição: {disc.descricao}| sE: {disc.segmentoEnsino}| professor: {disc.professor} ')
        else:
            print('Ocorreu um erro!')
            return     
    print(f'|| ({len(lista_disciplinas)+1}) - Sair')
    print(f'{"="*15}')
    try:
        disciplina_escolhida = lista_disciplinas[int(input('|| Digite o número da disciplina: ')) - 1]
    except:
        return None
    return disciplina_escolhida

def mostrar_professores(): 
    if len(lista_professores) == 0:
        return None
    print(f'Professores: \n{"="*15}')
    for prof in lista_professores:
        print(f'({lista_professores.index(prof)+1}) - Professor: {prof.nome} {prof.sobrenome} - {", ".join(prof.segmentoEnsino)}')
    print(f'({len(lista_professores)+1}) - Sair')
    print(f'{"="*15}')
    try:
        professor_escolhido = lista_professores[int(input('Digite o número do professor: ')) - 1]
    except:
        return None
    return professor_escolhido

def mostrar_disciplinas_especifico(turma):
    print(f'Disciplinas: \n{"="*15}')
    for disc in turma.disciplinas:
        print(f'({turma.disciplinas.index(disc)+1}) - Id: {disc.id} - {disc.descricao} - {disc.segmentoEnsino} - {disc.professor}')
    print(f'({len(turma.disciplinas)+1}) - Sair')
    print(f'{"="*15}')
    try:
        disciplina_escolhida = turma.disciplinas[int(input('Digite o número da disciplina: ')) - 1]
    except:
        return None
    return disciplina_escolhida
class Pessoa:
    def __init__(self, nome, sobrenome, endereco, user, email, senha, segmentoEnsino: list,turmas : list):
        self.nome = nome
        self.sobrenome = sobrenome
        self.__endereco = endereco
        self.user = user
        self.segmentoEnsino = segmentoEnsino
        self.email = email
        self.__senha = senha
        self.turmas = turmas

    @property
    def senha(self):
        return self.__senha
    @senha.setter
    def senha (self,senha):
        self.__senha = senha

    @property
    def endereco(self):
        return self.__endereco
    @endereco.setter
    def endereco (self,endereco):
        self.__endereco = endereco
    
class Aluno(Pessoa):
    def __init__(self, nome, sobrenome, endereco, filiacao, emailResponsavel, registroAcademico,segmentoEnsino, turmas, user, email, senha):
        super().__init__(nome, sobrenome, endereco, user, email, senha, segmentoEnsino, turmas)
        self.filiacao = filiacao
        self.emailResponsavel = emailResponsavel
        self.registroAcademico = registroAcademico


    def trocar_turma(self,nova_turma):
        if self not in nova_turma.alunos:
            if self.segmentoEnsino == "EM" and nova_turma.segmentoEnsino == "EM":
                self.turmas = nova_turma
                print(f'|| Turma trocada para {nova_turma.nome} ')
            
            elif self.segmentoEnsino == "Superior" and nova_turma.segmentoEnsino == "Superior":
                answ = input("|| Sair de algum curso? \n|| - (1) Sim\n|| - (2) Não\n|| Resposta(número): ")
                if answ == '1':
                    print(f"|| Digite o número do curso para sair dele:")
                    for turma in self.turmas:
                        print(f"|| Curso número {self.turmas.index(turma)+1}: {turma.nome}")
                        answ2 = input('|| Deseja sair do curso? \n|| - (1) Sim\n|| - (2) Não\nResposta(número):  ')
                        if answ2 == '1' :
                            self.turmas.remove(turma)
                            turma.alunos.remove(self) if self in turma.alunos else 0
                self.turmas.append(nova_turma)
                nova_turma.alunos.append(self)
                return(f'Suas turmas: {self.turmas}')
            else:
                print("Transferência para o segmento diferente não permitida.")
        else:
            print('Aluno já está na turma!')
            return False
    def __str__(self):
        f"""
Nome: {self.nome}
Sobrenome: {self.sobrenome}
Endereço: {self.endereco}
Filiação: {self.filiacao}
E-mail do Responsável: {self.emailResponsavel}
Registro Acadêmico: {self.registroAcademico}
Segmento de Ensino: {self.segmentoEnsino}
Turmas: {self.turmas}
Usuário: {self.user}
E-mail: {self.email}
Senha: {self.senha}
"""
        
class Professor(Pessoa):
    def __init__(self, nome, sobrenome, endereco, user, email, senha, formacoes, disciplinas : list, segmentoEnsino : list, turmas : list): #Segmento: Ensino Med ou Ensino Sup
        super().__init__(nome, sobrenome, endereco, user, email, senha, segmentoEnsino, turmas)
        self.formacoes = formacoes
        self.disciplinas = disciplinas


class Turma:
    def __init__(self, nome, segmentoEnsino, curso, anoEscolar,alunos : list, professores : list, disciplinas : list):
        self.nome = nome
        self.segmentoEnsino = segmentoEnsino
        self.__curso = curso
        self.anoEscolar = anoEscolar
        self.__alunos = alunos
        self.professores = professores
        self.__disciplinas = disciplinas
    
    @property
    def curso(self):
        return self.__curso
    @curso.setter
    def disciplinas (self,curso):
        self.__curso = curso

    @property
    def disciplinas(self):
        return self.__disciplinas
    @disciplinas.setter
    def disciplinas (self,disciplinas):
        self.__disciplinas = disciplinas
    
    @property
    def alunos(self):
        return self.__alunos
    @alunos.setter
    def alunos(self,alunos):
        self.__alunos = alunos

    def adicionar_aluno(self, aluno):
        if aluno.segmentoEnsino != self.segmentoEnsino:
            print("O segmento do aluno não corresponde ao da turma.")
        else:
            self.alunos.append(aluno)

    def verificar_minimo_alunos(self):
        if self.segmentoEnsino == "EM" and len(self.alunos) < 20:
            return False
        
        elif self.segmentoEnsino == "Superior" and len(self.alunos) < 5:
            return False
        else:
            return True
            
    def adicionar_professor(self,professor):
        self.professores.append(professor)
    
    def mostrar_alunos_que_faltam(self):
        if self.segmentoEnsino == "EM" and len(self.__alunos) < 20:
            print(f"Faltam {20-len(self.__alunos)} alunos para criar a turma do EM!")
    
        elif self.segmentoEnsino == "Superior" and len(self.__alunos) < 5 :
            print(f"Faltam {5-len(self.__alunos)} alunos para criar a turma do Superior!")

    def listar_alunos(self):
        for aluno in self.alunos:
            print(f'({self.alunos.index(aluno)+1}) - Nome: {aluno.nome} {aluno.sobrenome} - {aluno.segmentoEnsino} - {aluno.registroAcademico}')
        try:
            aluno_escolhido = self.alunos[int(input('Digite o número do aluno à inserir informações: ')) - 1]
        except:
            return
        return aluno_escolhido


class Disciplina:
    def __init__(self,id,descricao,segmentoEnsino,professor):
        self.__id = id
        self.__descricao = descricao
        self.segmentoEnsino = segmentoEnsino
        self.professor = professor
    
    @property
    def id(self):
        return self.__id
    @id.setter
    def id (self,id):
        self.__id = id
    
    @property
    def descricao(self):
        return self.__descricao
    @descricao.setter
    def descricao(self,descricao):
        self.__descricao = descricao

    def colocar_professor(self,professor):
        self.professor = professor
        return ('Professor adicionado na disciplina!')

lista_turmas = []
lista_disciplinas = []
lista_professores = []
cursoEM = ['mecatrônica', 'eletromecânica', 'informática']
cursoSup = ['ciências da computação' ,'pedagogia']
opcoes =  ['1','2','3','4','5']
lista_opc_menu1 = ['Turma','Disciplina','Aluno','Professor','Sair']
lista_opc_menu2 = ['Inserir','Editar','Excluir','Sair']

# Menu princial de operações (Escolha da classe à editar)

    # Função que define o menu principal
def menu_principal():
    while True:
        print(f"{'='*25}\n||   Menu Principal    {'|'*2}\n||{'='*21}||")
        for opc in lista_opc_menu1:    
            print(f"|| - ({lista_opc_menu1.index(opc)+1}) {opc}{' '*(14-len(opc))}||")
        print(f"||{'='*21}||")
        
        opcao_classe = (input(f"|| Resposta (número):  "))
        print('')
        if opcao_classe not in opcoes:
            print('\nEscolha uma opção disponível! ')
            time.sleep(1)
            continue
        
        elif opcao_classe == '5':
            print('Fim do código')
            return opcao_classe
        
        elif len(lista_turmas) == 0 and opcao_classe != '1': 
            print('\nCrie uma turma primeiro!')
            time.sleep(1)
            continue
        
        elif len(lista_disciplinas) == 0 and opcao_classe not in ['1','2']:
            print('\nCrie uma disciplina primeiro!')
            time.sleep(1)
            continue
        
        else:
            return opcao_classe

    # Função que define o menu secundário
def menu_secundario():
    while True:
        print(f"{'='*25}\n||   Menu Secundário   ||\n||{'='*21}||")
        for opc in lista_opc_menu2:    
            print(f"|| - ({lista_opc_menu2.index(opc)+1}) {opc}{' '*(14-len(opc))}||")
        
        opcao1 = input('|| Resposta (número):  ') #3 tirar da lista de alunos da turma
        if opcao1 not in ['1','2','3','4']:
            print('\nDigite uma opção disponível!')
            time.sleep(1)
            continue
        return opcao1

def inserir(opcao_classe):

    match opcao_classe:

        case '1':
            print(f'{"="*25}\n||       Inserir       ||\n||{"="*21}')
            print(f'|| Turma {len(lista_turmas)+1}...')
            nome = input("|| Digite o nome da turma: ")
            
            while True:
                segmentoEnsino = (input(f'{"="*25}\n|| Digite o número do segmento de ensino:\n|| - (1) EM\n|| - (2) Superior\n||{"="*23}\n|| Resposta (número): '))
                print('='*25)
                match segmentoEnsino:
                    case '1': 
                        if len(cursoEM) == 0:
                            print('\nLimite de turmas de ensino médio atingido!')
                            time.sleep(1)
                            break
                        segmentoEnsino = 'EM'
                        for c in cursoEM:
                            print(f'|| - ({cursoEM.index(c)+1}) {c}   ')
                        print(f'||{"="*23}')
                        opcao2 = int(input('|| Escolha o curso: '))
                        curso = cursoEM[opcao2-1]
                        cursoEM.remove(curso)

                    case '2': 
                        if len(cursoSup) == 0:
                            print('\nLimite de turmas de curso superior atingido!')
                            time.sleep(1)
                            break
                        segmentoEnsino = 'Superior'
                        for c in cursoSup:
                            print(f'|| - ({cursoSup.index(c)+1}) {c}   ')
                        opcao2 = int(input('|| Escolha o curso: '))
                        curso = cursoSup[opcao2-1]
                        cursoSup.remove(curso)
                    case _:
                        print('\nOpção inválida. Tente novamente!')
                        time.sleep(1)
                        continue
                ano = input(f'{"="*25}\n|| Digite o ano escolar: ')
                turma = Turma(nome,segmentoEnsino,curso,ano,[],[],[])
                lista_turmas.append(turma)
                while True:
                    opcao3 = (input(f'{"="*25}\n|| Deseja criar mais turmas?\n|| - (1) Sim\n|| - (2) Não\n||{"="*23}\n|| Resposta (número): '))
                    if opcao3 == '1':
                        for turma in lista_turmas:
                            print(turma.nome)
                        inserir(opcao_classe)
                        break
                    elif opcao3 == '2':
                        print('\nSaindo para o menu principal...')
                        time.sleep(1)
                        break
                                
                    else:
                        print('\nOpção inválida. Tente novamente')
                        continue
                break
                        
# Disciplina           
        case '2':
            print(f'{"="*25}\n||       Inserir       ||\n||{"="*21}')
            print(f'|| Disciplina {len(lista_disciplinas)+1}...')
            while True:
                id = input(f'{"="*25}\n||Digite o id: ')
                descricao = input(f'{"="*25}\n|| Digite a descrição da disciplina: ')
                segmentoEnsino = ''
                while segmentoEnsino not in ['EM','Superior']:
                    segmentoEnsino = (input(f'{"="*25}\n|| Digite o número do segmento de ensino:\n|| - (1) EM\n|| - (2) Superior\n||{"="*23}\n|| Resposta (número): '))

                    match segmentoEnsino:
                        case '1':
                            segmentoEnsino = 'EM'
                        case '2':
                            segmentoEnsino = 'Superior'
                        case _:
                            print('\nOpção inválida. Tente novamente!')
                            time.sleep(1)
                disciplina = Disciplina(id,descricao,segmentoEnsino,None)
                
                while True:
                    turma_escolhida =  mostrar_turmas()

                    if turma_escolhida == None:
                        print('\nVocê escolheu sair... [Disciplina não criada (necessário adicionar em uma turma para validar! )]')
                        time.sleep(1)
                        break

                    if disciplina not in turma_escolhida.disciplinas and turma_escolhida.segmentoEnsino == disciplina.segmentoEnsino: 
                        turma_escolhida.disciplinas.append(disciplina)
                        lista_disciplinas.append(disciplina) if disciplina not in lista_disciplinas else 0
                        print('Disciplina criada!')
                        time.sleep(1)
                    elif disciplina in turma_escolhida.disciplinas:
                        print('Essa disciplina já está nessa turma!')
                        time.sleep(1)
                        continue
                    
                    elif turma_escolhida.segmentoEnsino != disciplina.segmentoEnsino: 
                        print('Não é do mesmo segmento de ensino!')
                        time.sleep(1)
                        continue
                    
                    while True:    
                        opcao4 = (input(f'\n{"="*25}\n|| Deseja adicionar a disciplina em mais turmas?\n|| - (1) Sim\n|| - (2) Não\n||{"="*23}\n|| Resposta (número): '))
                        match opcao4:
                            case '1':
                                break
                        
                            case '2':
                                print('Continuando o programa...')
                                break
                                    
                            case _:
                                print('\nOpção inválida. Tente novamente!')
                                time.sleep(1)
                                continue
                                
                    if opcao4 == '2':
                        break
                while True:
                    opcao5 = (input(f'\n{"="*25}\n|| Deseja criar mais disciplinas?\n|| - (1) Sim\n|| - (2) Não\n||{"="*23}\n|| Resposta (número): '))
                    if opcao5 == '1':
                        for turma in lista_turmas:
                            print(turma.nome)
                        
                        inserir(opcao_classe)
                        break
                    elif opcao5 == '2':
                        print('Saindo para o menu principal...')
                        time.sleep(1)
                        break
                                
                    else:
                        print(lista_disciplinas)
                        print('Coloque um valor disponível!')
                        continue
                break           
            
                # Alunos 
        case '3':
            print(f'{"="*25}\n||       Inserir       ||\n||{"="*21}')
            print(f'|| Alunos... ')
            a = mostrar_turmas()
            if a == None:
                print('Você escolheu sair...')
            else:    
                if len(a.alunos) != 0: qtdd_alunos = len(a.alunos)  
                else: qtdd_alunos = 0
                print(f'{"="*25}\n|| Quantidade de alunos na turma: {qtdd_alunos}')
                while True:
                    forma = input(f'{"="*25}\n|| Escolha o método de inserção: \n|| - (1) Método rápido (fins de teste) \n|| - (2) Método manual \n||{"="*23}\n|| Resposta (número): ')
                    match forma:
                        case '1':
                            alunos = int(input(f'{"="*30}\n|| Quantidade de alunos: '))
                            for i in range(alunos):
                                nome = nomes[random.randint(0, 49)]
                                sobrenome = sobrenomes[random.randint(0, 49)]
                                endereco = enderecos[random.randint(0, 49)]
                                filiacao = filiacoes[random.randint(0, len(filiacoes) - 1)]
                                emailResponsavel = f"{filiacao}.{random.randint(1, 9999)}@gmail.com"
                                registroAcademico = registrosAcademicos[random.randint(0, 49)]
                                user = f'user_{nome}_escola'
                                email = f'{nome}.{sobrenome}@gmail.com'
                                senha = f'senha{random.randint(1000, 99999999)}'
                                segmentoEnsino = a.segmentoEnsino
                                turmas = [a]
                                aluno = Aluno(nome, sobrenome, endereco, filiacao, emailResponsavel, registroAcademico, segmentoEnsino, turmas, user, email, senha)

                                a.adicionar_aluno(aluno)
                                if len(a.alunos) > 45:
                                    print(f'\nLimite de alunos atingido!')
                                    break
                            if a.verificar_minimo_alunos():
                                while True:
                                    opcao6 = input(f'\n{"="*25}\n|| Deseja criar mais alunos? ||\n|| - (1) Sim \n|| - (2) Não \n||{"="*23}\n|| Resposta (número): ')
                                    match opcao6:
                                        case '1':
                                            inserir(opcao_classe)
                                            break
                                        case '2':
                                            print(f'\nSaindo para o menu principal... ')
                                            time.sleep(1)
                                            break
                                        case _:
                                            print(f'\nOpção inválida. Tente novamente! ')
                                            time.sleep(1)
                                            continue
                            else:
                                a.mostrar_alunos_que_faltam()
                                continue
                            break

                        case '2':
                            while True:
                                nome = input(f'{"="*30}\n|| Digite o nome (ou número para terminar): ')
                                try:
                                    int(nome)
                                    if a.verificar_minimo_alunos():
                                        break
                                    else:
                                        a.mostrar_alunos_que_faltam()
                                        continue
                                except ValueError:
                                    pass

                                sobrenome = input("|| Digite o sobrenome: ")
                                endereco = input("|| Digite o endereço: ")
                                filiacao = input("|| Digite a filiação (ex.: Pai, Mãe, Tutor, etc.): ")
                                emailResponsavel = input("|| Digite o e-mail do responsável: ")
                                registroAcademico = input("|| Digite o registro acadêmico: ")
                                user = input("|| Digite o nome de usuário: ")
                                email = input("|| Digite o e-mail: ")
                                senha = input("|| Digite a senha: ")
                                segmentoEnsino = a.segmentoEnsino
                                turmas = [a]
                                aluno = Aluno(nome, sobrenome, endereco, filiacao, emailResponsavel, registroAcademico, segmentoEnsino, turmas, user, email, senha)
                                a.adicionar_aluno(aluno)

                                if len(a.alunos) >= 45:
                                    print(f'\nLimite de alunos atingido!')
                                    break

                        case _:
                            print(f'\nOpção inválida. Tente novamente! ')
                            time.sleep(1)
                            continue
                    break

        #PROFESSORES
        case '4':
            while True:        
                print(f'{"="*25}\n|| Inserir Professor   ||\n{"="*25}')
                nome = input("|| Digite o nome: ")
                sobrenome = input("|| Digite o sobrenome: ")
                endereco = input("|| Digite o endereço: ")
                user = input("|| Digite o nome de usuário: ")
                email = input("|| Digite o e-mail: ")
                senha = input("|| Digite a senha: ")
                formacoes = []
                
                while True:
                    formacao = input("|| Digite a(s) formação(ões), (numeral para terminar): ")
                    try:
                        int(formacao)
                        break
                    except ValueError:
                        formacoes.append(formacao) 
                professor = Professor(nome, sobrenome, endereco, user, email, senha, formacoes, [], [], [])                

                while True:    
                    disciplina = mostrar_disciplinas()
                    if disciplina is None:
                        print(f'\nVocê escolheu sair...')
                        break
                    if disciplina not in professor.disciplinas:
                        professor.disciplinas.append(disciplina)
                        print(f'{"="*25}\n|| Disciplina adicionada ao professor!')
                    else:
                        print(f'{"="*25}\n|| Essa disciplina já está cadastrada nesse professor!')
                    disciplina.professor = professor

                    for tur in lista_turmas:
                        if disciplina in tur.disciplinas:
                            if tur not in professor.turmas:
                                professor.turmas.append(tur)
                                if professor not in tur.professores:
                                    tur.professores.append(professor)
                                    print('O professor foi add na turma ',tur.nome)
                                print(f'|| Turma {tur.nome} foi adicionada!')
                    
                    while True:   
                        opcao7 = input(f'{"="*25}\n|| Deseja adicionar o professor em mais disciplinas?\n|| - (1) Sim\n|| - (2) Não\n||{"="*23}\n|| Resposta (número): ')
                        match opcao7:
                            case '1': 
                                break
                            case '2':
                                print(f'\nContinuando o programa...')
                                break
                            case _:
                                print(f'\n Opção inválida. Tente novamente! ')
                                time.sleep(1)
                                continue
                            
                    if opcao7 == '2':
                        break

                for disciplina in professor.disciplinas:
                    if disciplina.segmentoEnsino not in professor.segmentoEnsino:
                        professor.segmentoEnsino.append(disciplina.segmentoEnsino)
                    

                lista_professores.append(professor)    
                while True:
                    opcao8 = input(f'\n{"="*25}\n|| Deseja criar mais professores? \n|| - (1) Sim\n|| - (2) Não\n||{"="*23}\n|| Resposta (número): ')
                    match opcao8:
                        case '1': 
                            inserir(opcao_classe)
                            break
                        case '2': 
                            print(f'\nSaindo para o menu principal...')
                            time.sleep(1)
                            break
                        case _:
                            print(f'\nOpção inválida. Tente novamente!')
                            time.sleep(1)
                
                break

def editar(opcao_classe):
    
    match opcao_classe:
        
        case '1':#Editar turma
            print("Editar: ")
            while True:
                if len(lista_turmas) == 0:
                    print('****Crie uma turma primeiro!****')
                    break

                turma = mostrar_turmas()

                if turma == None:
                    print('\nVocê escolheu sair...')
                    break
                
                # Solicitar dados da turma a ser editada
                print(f"\n{'='*25}\n|| Opções de edição para a Turma:")
                print("|| - (1) Nome")
                print("|| - (2) Ano Escolar")
                print("|| - (3) Disciplinas")
                print("|| - (4) Sair")
                print("||"+"="*23)

                opcao = (input("|| Digite o número da opção que deseja editar: "))
                print('='*25)
                match opcao:
                    case '1':
                        novo_nome = input("|| Digite o novo nome da turma: ")
                        turma.nome = novo_nome
                        print(f"O nome da turma foi atualizado para {turma.nome}.")
                        time.sleep(1)
                    case '2':
                        novo_ano = input("||Digite o novo ano escolar: ")
                        turma.anoEscolar = novo_ano
                        print(f"\nO ano escolar foi atualizado para {turma.anoEscolar}.")
                        time.sleep(1)

                    case '3':
                        print("|| Editar disciplinas da turma: ")
                        print('|| - (1) Adicionar')
                        print('|| - (2) Excluir')
                        print('|| - (3) Sair')
                        resp = (input("Digite o número da opção desejada: "))

                        match resp:
                            case '1':
                                disciplina = mostrar_disciplinas()                                                            
                                if disciplina == None:
                                    print('\nVocê escolheu sair...')
                                    time.sleep(1)
                                    break
                                if disciplina.segmentoEnsino == turma.segmentoEnsino:
                                    turma.disciplinas.append(disciplina)  
                                else: 
                                    print('Não é do mesmo segmento de ensino')
                                    time.sleep(1)
                                    continue
                                if disciplina.professor != None:
                                    disciplina.professor.turmas.append(turma) 
                                    print(f'O professor {professor.nome} recebeu a turma {turma.nome}')
                                print(f'A disciplina {disciplina.id} foi adicionada à turma!')
                                
                            case '2':
                                disciplina = mostrar_disciplinas_especifico(turma) 
                                if disciplina == None:
                                    print('\nVocê escolheu sair...')
                                    break
                                
                                turma.disciplinas.remove(disciplina)
                                print(f'A disciplina {disciplina.id} foi removida da turma!')                               
                            
                            case '3':
                                print('\nVocê escolheu sair...')
                                break
                            
                            case _:
                                print('\nOpção inválida.')
                                break

                    case '4':
                        print('\nVocê escolheu sair...')
                        break
                    
                    case _:
                        print('\nOpção inválida. Tente novamente!')
                        time.sleep(1)
                        continue
        case '2':#Editar disciplina
            print("Editar: ")
            
            while True:
            
                disciplina = mostrar_disciplinas()
                if disciplina == None:
                    print('\nVocê escolheu sair...')
                    break
                
                elif len(lista_disciplinas) > 0:
                    print("Opções de edição para a Disciplina:")
                    print("1. ID")
                    print("2. Descrição")
                    print("3. Sair")
                

                    opcao = input("Digite o número da opção que deseja editar: ")
                    match opcao:
                        case "1":
                            novo_id = input("Digite o novo ID da disciplina: ")
                            disciplina.id = novo_id
                            print(f"O ID da disciplina foi atualizado para {disciplina.id}.")

                        case "2":
                            nova_descricao = input("Digite a nova descrição da disciplina: ")
                            disciplina.descricao = nova_descricao
                            print(f"A descrição da disciplina foi atualizada para '{disciplina.descricao}'.")

                        case "3":
                            print("Você escolheu sair...")
                            break

                        case _:
                            print("\nOpção inválida. Tente novamente.")
                elif len(lista_disciplinas) == 0:
                    print('****Crie uma disciplina primeiro!****')
                    break
                elif disciplina == None:
                    print('\nVocê escolheu sair...')

        case '3':#/Editar aluno
            print("Editar aluno: \nEscolha a turma para editar os seus alunos:")
            
            while True:

                turma = mostrar_turmas()
                if turma == None:
                    print('Você escolheu sair/ocorreu um erro!')
                    break
                aluno = turma.listar_alunos()
                if len(turma.alunos) > 0:
                    

                    while True:
                        print(f'Editar alunos da turma {turma.nome} - {turma.segmentoEnsino}: ')
                        print("Opções de edição para o Aluno:")
                        print("1. Nome")
                        print("2. Sobrenome")
                        print("3. Endereço")
                        print("4. Filiação")
                        print("5. E-mail do Responsável")
                        print("6. Registro Acadêmico")
                        print("7. Turmas")
                        print("8. Sair")
                        
                        opcao = (input(f"Digite o número da opção que deseja editar para o aluno {aluno.nome} {aluno.sobrenome}: "))
        
                        match opcao:
                            case '1':
                                novo_nome = input("Digite o novo nome do aluno: ")
                                aluno.nome = novo_nome
                                print(f"O nome do aluno foi atualizado para {aluno.nome}.")

                            case '2':
                                novo_sobrenome = input("Digite o novo sobrenome do aluno: ")
                                aluno.sobrenome = novo_sobrenome
                                print(f"O sobrenome do aluno foi atualizado para {aluno.sobrenome}.")

                            case '3':
                                novo_endereco = input("Digite o novo endereço do aluno: ")
                                aluno.endereco = novo_endereco
                                print(f"O endereço do aluno foi atualizado para {aluno.endereco}.")

                            case '4':
                                for filiacao in filiacoes:
                                    print(f'({filiacoes.index(filiacao)+1}) - {filiacao}')
                                resp = int(input("Digite o número correspondente à filiação desejada: ")) - 1
                                nova_filiacao = filiacoes[resp]
                                
                                aluno.filiacao = nova_filiacao
                                print(f"A filiação do aluno foi atualizada para {aluno.filiacao}.")

                            case '5':
                                novo_email_responsavel = input("Digite o novo e-mail do responsável: ")
                                aluno.emailResponsavel = novo_email_responsavel
                                print(f"O e-mail do responsável foi atualizado para {aluno.emailResponsavel}.")

                            case '6':
                                novo_ra = input("Digite o novo registro acadêmico do aluno: ")
                                aluno.ra = novo_ra
                                print(f"O registro acadêmico do aluno foi atualizado para {aluno.ra}.")

                            case '7':
                                print(f'{"="*25}\n|| Adicionar aluno na turma: ')
                                turma_escolhida = mostrar_turmas()
                                aluno.trocar_turma(turma_escolhida)

                            case '8':
                                print("Você escolheu sair...")
                                break

                            case _:
                                print("\nOpção inválida. Tente novamente.")
                                continue
                        break
                
                elif len(turma.alunos) > 0:
                    print("Adicione alunos à turma antes!")
                    break
                elif aluno == None:
                    print('\nVocê escolheu sair...')
                    break       
        case '4': #Editar professor
            while True:
                print("Editar: ")
                professor = mostrar_professores()
                
                if len(lista_professores) == 0:
                    print("Crie um professor primeiro")
                    break
                
                elif professor == None:
                    print('\nVocê escolheu sair...') 
                    break
                
                print_formacao = ", ".join(professor.formacoes)
                print_disciplina = []
                print_turma = []
                
                for disciplina in professor.disciplinas:
                    print_disciplina.append(disciplina.id)
                for turma in professor.turmas:
                    print_turma.append(turma.nome)
                    
                print_disciplina = ", ".join(print_disciplina)
                print_turma = ", ".join(print_turma)
                
                
                print(f"Opções de edição para o Professor:")
                print(f"- (1) Nome: {professor.nome}")
                print(f"- (2) Sobrenome:  {professor.sobrenome}")
                print(f"- (3) Endereço:{professor.endereco}")
                print(f"- (4) Formações: {print_formacao}")
                print(f"- (5) Disciplinas: {print_disciplina}")
                print(f"- --- Turmas: {print_turma}")
                print(f"- (6) Senha: {professor.senha}")
                print(f"- (7) Sair")

                opcao = input("Digite o número da opção que deseja editar: ")

                match opcao:
                    case "1":
                        novo_nome = input("Digite o novo nome do professor: ")
                        professor.nome = novo_nome
                        print(f"O nome do professor foi atualizado para {professor.nome}.")

                    case "2":
                        novo_sobrenome = input("Digite o novo sobrenome do professor: ")
                        professor.sobrenome = novo_sobrenome
                        print(f"O sobrenome do professor foi atualizado para {professor.sobrenome}.")

                    case "3":
                        novo_endereco = input("Digite o novo endereço do professor: ")
                        professor.endereco = novo_endereco
                        print(f"O endereço do professor foi atualizado para {professor.endereco}.")

                    case "4":
                        print("- (1) Adicionar formações")
                        print("- (2) Remover formações")
                        print("- (3) Substituir todas as formações")
                        sub_opcao = input("Digite o número da opção que deseja editar: ")
                        
                        match sub_opcao:
                        
                            case "1":
                                while True:
                                    formacao = input("Digite a(s) novas formação(ões), (numeral para terminar):")
                                    try:
                                        int(formacao)
                                        break
                                    except (ValueError):
                                        professor.formacoes.append(formacao) 
                            
                            case"2":
                                print("As formações atuais do professor são: ")
                                for i in range(len(professor.formacoes)):
                                    print(f"({i+1}) - {professor.formacoes[i]}")
                                    
                                remover_formacao = input("Digite o número da formação que deseja remover: ")
                                professor.formacoes.pop(int(remover_formacao) - 1)
                            
                            case "3":
                                professor.formacoes = []
                                while True:
                                    formacao = input("Digite a(s) novas formação(ões), (numeral para terminar):")
                                    try:
                                        int(formacao)
                                        break
                                    except (ValueError):
                                        professor.formacoes.append(formacao)
                                        
                    case "5":
                        print("1. Adicionar uma disciplina")
                        print("2. Remover uma disciplina")
                        sub_opcao = input("Digite a opção desejada: ")

                        match sub_opcao:
                            case "1":
                                disciplina_escolhida = mostrar_disciplinas()
                                if disciplina_escolhida == None:
                                    print('\nVocê escolheu sair...')
                                    break

                                
                                for tur_prof in lista_turmas:
                                    
                                    for dis_tur_prof in tur_prof.disciplinas:
                                        
                                        if dis_tur_prof == disciplina_escolhida:
                                            if tur_prof not in professor.turmas:
                                                professor.turmas.append(tur_prof)
                                                print(f"Turma '{tur_prof.nome}' adicionada ao professor!") 
                                                break

                                if disciplina_escolhida not in professor.disciplinas and disciplina_escolhida != None:
                                    professor.disciplinas.append(disciplina_escolhida)
                                    professor.segmentoEnsino.append(disciplina_escolhida.segmentoEnsino) if disciplina_escolhida.segmentoEnsino not in professor.segmentoEnsino else 0
                                    disciplina_escolhida.professor = professor
                                    print(f"Disciplina '{disciplina_escolhida.id}' adicionada.")

                                else:
                                    print('Essa disciplina já está cadastrada nesse professor.')
                                    
                            case "2":
                                if len(professor.disciplinas) == 0:
                                    print('O professor escolhido não possui disciplinas!')
                                    continue
                                print('Disciplinas: ')
                                for disciplina in professor.disciplinas:
                                    print(f'({professor.disciplinas.index(disciplina)+1}) - {disciplina.id} - {disciplina.segmentoEnsino}')
                                print(f'({len(professor.disciplinas)+1}) - Sair')
                                
                                try:
                                    disciplina_escolhida = professor.disciplinas[int(input('Digite o número da disciplina: ')) - 1]
                                except:
                                    print('\nVocê escolheu sair...')
                                    continue
                                
                                print(professor.segmentoEnsino)    
                                
                                
                                if disciplina_escolhida in professor.disciplinas:
                                    professor.disciplinas.remove(disciplina_escolhida)
                                    disciplina_escolhida.professor = None
                                    for tur_prof in professor.turmas:
                                        
                                        tem_disciplina_vinculada = False
                                        
                                        for dis_tur_prof in tur_prof.disciplinas:
                                            if dis_tur_prof in professor.disciplinas:
                                                tem_disciplina_vinculada = True
                                                break  
                                        
                                
                                        if tem_disciplina_vinculada == False:
                                            professor.turmas.remove(tur_prof)
                                            print(f"Turma '{tur_prof.nome}' removida!")
                                            
                                    verify = False
                                    for disc_prof in professor.disciplinas:
                                        if disc_prof.segmentoEnsino == disciplina_escolhida.segmentoEnsino:
                                            verify = True
                                            break  

                                    if not verify:
                                        professor.segmentoEnsino.remove(disciplina_escolhida.segmentoEnsino)


                                    print(f"Disciplina '{disciplina_escolhida.id}' removida.")
                                
                                else:
                                    print("Disciplina não encontrada.")
                                    
                            case _:
                                print("\nOpção inválida.")
                    
                    case "6":
                        nova_senha = input("Digite a nova senha do professor: ")
                        professor.senha = nova_senha
                        print("A senha do professor foi atualizada com sucesso.")
                    
                    case "7":
                        print("Você escolheu sair...")
                        break

                    case _:
                        print("\nOpção inválida. Tente novamente.")
                

            
        case _:
            print('\nOpção inválida. Tente novamente!')
            time.sleep(1)   

def excluir(opcao_classe):
    match opcao_classe:
        
        case '1': #excluir turma

            while True:
                print('Excluir: ')
                print('Turma: ')
                if len(lista_turmas) == 0:
                    print('****Crie uma turma primeiro!****')
                    break
                print('Digite o número da turma para excluir:')
                turma_escolhida = mostrar_turmas()
                
                if turma_escolhida == None:
                    print('\nVocê escolheu sair...')
                    break
                    
                elif turma_escolhida.segmentoEnsino == 'EM':
                    cursoEM.append(turma_escolhida.curso)
                    print('Lista de cursos em EM: ',cursoEM)
                else:
                    cursoSup.append(turma_escolhida.curso)
                    print('Lista de cursos em Superior: ',cursoSup)
                
                
                for professor in turma_escolhida.professores:
                    professor.turmas.remove(turma_escolhida)

                    for disciplina in turma_escolhida.disciplinas:
                        disciplina_associada = False
                        for outra_turma in professor.turmas:
                            if disciplina in outra_turma.disciplinas:
                                disciplina_associada = True
                                break
                        

                        if not disciplina_associada:
                            professor.disciplinas.remove(disciplina)
                            
                segs = []
                for disc in professor.disciplinas:
                    segs.append(disc.segmentoEnsino)  
                    
                for segmento in professor.segmentoEnsino:
                    if segmento not in segs:
                        professor.segmentoEnsino.remove(segmento)
                        
                lista_turmas.remove(turma_escolhida)
                
                while True:
                    opcao = (input(f'\n{"="*15}\nDeseja excluir mais uma turma?\n1 - Sim\n2 - Não\n{"="*15}\nResposta (número): '))
                    match opcao:
                        case '1': 
                            break
                        case '2': 
                            print('\nVocê escolheu sair...')
                            break
                        case _:
                            print('\nOpção inválida. Tente novamente!')
                            time.sleep(1)
                            continue
                if opcao == '2': 
                    break
                    
        case '2': # excluir disciplina
            
            while True:
                print("Excluir: ")
                print("Disciplina: ")
                if len(lista_disciplinas) == 0:
                    print('**** Crie uma disciplina primeiro! **** ')
                    break
                    
                disciplina = mostrar_disciplinas()
                
                if disciplina == None:
                    print('\nVocê escolheu sair...')
                    break
                    
                for turma in lista_turmas:
                    for discip in turma.disciplinas:
                        if discip == disciplina:
                            turma.disciplinas.remove(discip)

                            interligado = False
                            for d in discip.professor.disciplinas:
                                if d in turma.disciplinas:  # Se o professor tiver outra disciplina na turma
                                    interligado = True
                                    break

                            
                            if not interligado:
                                discip.professor.turmas.remove(turma)

                disciplina.professor.disciplinas.remove(disciplina)
                lista_disciplinas.remove(disciplina)

                segs = []
                for disc in disciplina.professor.disciplinas:
                    segs.append(disc.segmentoEnsino)  
                    
                for segmento in disciplina.professor.segmentoEnsino:
                    if segmento not in segs:
                        disciplina.professor.segmentoEnsino.remove(segmento)
                
                while True:
                        opcao = (input(f'\n{"="*15}\nDeseja excluir mais uma disciplina?\n1 - Sim\n2 - Não\n{"="*15}\nResposta (número): '))
                        match opcao:
                                case '1': 
                                    break
                                case '2': 
                                    print('Saindo para o menu principal...')
                                    time.sleep(1)
                                    break
                                case _:
                                    print('\nOpção inválida. Tente novamente!')
                                    time.sleep(1)
                                    continue
                if opcao == '2': 
                    break

        case '3': #excluir aluno
            while True:
                print('Excluir: ')
                print("Excluir Aluno")
                

                print("Digite o número da turma para excluir")
                turma = mostrar_turmas()
                if turma == None:
                    print('Você escolheu sair...')
                    break
                
                
                if len(turma.alunos) == 0:
                    print('**** Crie os alunos primeiro!**** ')
                    break
                
                        
                for alu in turma.alunos:
                    print(f'({turma.alunos.index(alu)+1}) - {alu.nome} {alu.sobrenome}')
                    
                opcao = int(input(f'\n{"="*15}\nResposta (número): '))
                aluno = turma.alunos[opcao-1]
                for turma in lista_turmas:
                    for alun in turma.alunos:
                        if alun == aluno:
                            turma.alunos.remove(aluno)
                        
                            
                
                while True:
                    opcao = (input(f'\n{"="*15}\nDeseja excluir mais um aluno?\n1 - Sim\n2 - Não\n{"="*15}\nResposta (número): '))
                    match opcao:
                            case '1': 
                                break
                            case '2': 
                                print('\nVocê escolheu sair...')
                                break
                            case _:
                                print('\nOpção inválida. Tente novamente!')
                                time.sleep(1)
                                continue
                if opcao == '2': 
                    break           
                
        case '4': # excluir professor
            print("Excluir: ")
            print("Professor: ")
            while True:
                if len(lista_professores) == 0:
                    print('**** Crie um professor primeiro!**** ')
                    break
                if len(lista_professores ) > 1:
                    print("Digite o número do professor para excluir")
                    
                for prof in lista_professores:
                    print(f'({lista_professores.index(prof)+1}) - {prof.nome} {prof.sobrenome}')
                    
                opcao = int(input(f'\n{"="*15}\nResposta (número): '))
                professor = lista_professores[opcao-1]
            
                for turma in lista_turmas:
                    for prof in turma.professores:
                        if prof == professor:
                            turma.professores.remove(prof)
                for disc in lista_disciplinas:
                    if professor == disc.professor:  
                        disc.professor = None
                    else:
                        pass
                
                lista_professores.remove(prof)
                print(turma.professores, len(turma.professores))
                print(prof)
                while True:
                        opcao = (input(f'\n{"="*15}\nDeseja excluir mais um professor?\n1 - Sim\n2 - Não\n{"="*15}\nResposta (número): '))
                        match opcao:
                                case '1': 
                                    break
                                case '2': 
                                    print('Saindo para o menu principal...')
                                    time.sleep(1)
                                    break
                                case _:
                                    print('\nOpção inválida. Tente novamente!')
                                    time.sleep(1)
                                    continue
                if opcao == '2': 
                    break
while True:    
    resp_menu = menu_principal()
    if resp_menu == '5':
        break
    
    resp_menu2 = menu_secundario()
    if resp_menu2 == '1':
        inserir(resp_menu)
    
    elif resp_menu2 == '2':
        editar(resp_menu)
        
    elif resp_menu2 == '3':
        excluir(resp_menu)
    elif resp_menu2 == '4':
        pass
