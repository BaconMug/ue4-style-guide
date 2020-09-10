# Guia de Estilo UE4

*Uma abordagem rasoavelmente adequada para a Unreal Engine 4*

Traduzido e adaptado deste [guia](https://github.com/Allar/ue4-style-guide)

## Unreal Engine 4 Linter Plugin

Um método automatico para checar o seu projeto está de acordo com este guia esta disponivel no [Marketplace](https://www.unrealengine.com/marketplace/en-US/product/linter-v2).

## Linter e Documentação do Guia de Estilo

A documentação mais técnica sobre o plugin e este Guia de Estilo pode ser encontrada neste [link](https://ue4-style-guide.readthedocs.io/en/latest/).

## Terminologia Importante

##### Levels/Maps

A palavra "map" geralmente se refere ao que uma pessoa comum chama de "level" que pode ser usada também sem problemas. Veja um histórico do termo [aqui](https://en.wikipedia.org/wiki/Level_(video_gaming)).

##### Cases

Existem algumas diferentes formas que você pode usar para nomear coisas. Os tipos de cases mais comuns são:

> ###### PascalCase
>
> Coloque em maiúsculo toda primeira letra de cada palavra e remova espaços e caracteres especiais: `DesertEagle`, `StyleGuide`, `ASeriesOfWords`.
> 
> ###### camelCase
>
> A primeira letra da primeira palavra sempre será minuscula e todas as próximas palavras começam com maiúscula: `desertEagle`, `styleGuide`, `aSeriesOfWords`.
>
> ###### Snake_case
>
> Palavras podem começar com maiúscula ou minúscula mas as palavras são separadas por underline: `desert_Eagle`, `Style_Guide`, `a_Series_of_Words`.

##### Variaveis / Propriedades

As palavras "variável" e "propriedade" na maioria dos contextos se referem a mesma coisa. Mas se ambas forem usadas no mesmo contexto:

###### Propriedade
Normalmente se refere a uma variável definida dentro de uma classe. Por exemplo, se `BP_Barrel` tem uma variável `bExploded`, `bExploded` pode ser referida com uma propriedade do `BP_Barrel`. 

Quando usada no contexto de uma classe, é mais usado para dizer que você está acessando uma informação definida anteriormente.

###### Variável
Normalmente se refere a  uma variável definida como um argumento de uma função ou uma variável local dentro de uma função.

Quando no contexto de uma classe, é mais usada para  discutir sobre uma definição e qual o valor que ela tem.

<a name="0"></a>
## 0. Princípios

Estes principios foram adaptados do [idomatic.js style guide](https://github.com/rwaldron/idiomatic.js/).

<a name="0.1"></a>
### 0.1 Se o seu projeto na Unreal já utiliza um Guia de Estilo, você deve segui-lo.

Se você está trabalhando em um projeto ou em um time que já tenha um Guia de Estilo pré-definido, você deve respeitá-lo. Qualquer inconsistência ente um Guia de Estilo atual e esse Guia de Estilo deve se preferir o que já existe.

Guias de Estilos devem sem documentos dinâmicos, no entanto você deve propor mudanças ao Guia de Estilo existente com base nesse guia se você achar que pode beneficiar todos os usos.

> #### "Argumentos contra estilos não tem sentido. Deve exister um guia de estilo, e você deve segui-lo."
> [_Rebecca Murphey_](https://rmurphey.com)

<a name="0.2"></a>
### 0.2 Toda as estrutura, assets e códigos em um projeto da Unreal Engine 4 deve parecer que foi escrito por uma única pessoa, Não importa quantas pessoas tenham contribuído.

Mudar de um projeto para outro não deve causar um reaprendizado de estilo e estrutura. A conformidade com um guia de estilo remove suposições e ambigüidades desnecessárias.

Também permite uma criação e manutenção mais produtivas, pois não é necessário pensar no estilo, basta seguir as instruções. Este guia de estilo foi escrito com as práticas recomendadas em mente, o que significa que, ao seguir este guia de estilo, você também minimizará problemas difíceis de controlar.

<a name="0.3"></a>
### 0.3 Amigos não deixam outros amigos terem um estilo ruim.

Se você vir alguém trabalhando contra um guia de estilo ou nenhum guia de estilo, tente corrigi-lo.

Ao trabalhar em uma equipe ou discutir em uma comunidade como [Unreal Slackers] (http://join.unrealslackers.org/), é muito mais fácil ajudar e pedir ajuda quando as pessoas são consistentes. Ninguém gosta de ajudar a desemaranhar o espaguete do Blueprint de alguém ou lidar com ativos com nomes que eles não conseguem entender.

Se você está ajudando alguém cujo trabalho segue um guia de estilo diferente, mas consistente e lógico, você deve ser capaz de se adaptar a ele. Se eles não estiverem de acordo com nenhum guia de estilo, indique-os esse guia de estilo.

<a name="0.4"></a>
### 0.4 Uma equipe sem um guia de estilo não é uma equipe minha.

Ao ingressar em uma equipe Unreal Engine 4, uma de suas primeiras perguntas deve ser "Você tem um guia de estilo?". Se a resposta for não, você deve ser cético quanto à capacidade deles de trabalhar em equipe.

<a name="0.5"></a>
### 0.5 Não quebre a lei.

Não somos advogados, mas por favor, não introduza ações e comportamentos ilegais em um projeto, incluindo, mas não se limitando a:

* Não distribua conteúdo para o qual você não tem os direitos de distribuição
* Não infrinja materiais com direitos autorais ou marca registrada de outra pessoa
* Não roube conteúdo
* Siga as restrições de licenciamento de conteúdo

<a name="toc"></a>
## Indice.

> 1. [Asset Naming Conventions](#anc)
> 1. [Directory Structure](#structure)
> 1. [Blueprints](#bp)
> 1. [Static Meshes](#s)
> 1. [Particle Systems](#ps)
> 1. [Levels / Maps](#levels)
> 1. [Textures](#textures)

<a name="anc"></a>
<a name="1"></a>
## 1. Asset Naming Conventions

As convenções de nomenclatura devem ser tratadas como lei. Um projeto que está em conformidade com uma convenção de nomenclatura pode ter seus assets gerenciados, pesquisados, analisados e mantidos com uma facilidade incrível.

Muitas coisas são prefixadas com prefixos sendo geralmente um acrônimo do tipo de asset seguido por um underline.

<a name="base-asset-name"></a>
<a name="1.1"></a>
### 1.1 Base Asset Name - `Prefix_BaseAssetName_Variant_Suffix`

Todos os assets devem ter um _BaseAssetName_. Um nome de asset representa um agrupamento lógico de assets relacionados. Qualquer asset que faça parte deste grupo lógico deve seguir o padrão de `Prefix_BaseAssetName_Variant_Suffix`.

Manter o padrão `Prefix_BaseAssetName_Variant_Suffix` em mente e usar o bom senso geralmente é suficiente para garantir bons nomes de assets. Aqui estão algumas regras detalhadas sobre cada elemento.

`Prefix` e` Suffix` devem ser determinados pelo tipo de asset por meio das seguintes tabela [Asset Name Modifier] (#asset-name-modifiers).

`BaseAssetName` deve ser determinado por um nome curto e facilmente reconhecível relacionado ao contexto deste grupo de assets. Por exemplo, se você tivesse um personagem chamado Bob, todos os recursos de Bob teriam o `BaseAssetName` de` Bob`.

Para variações exclusivas e específicas de assets, `Variant` é um nome curto e facilmente reconhecível que representa o agrupamento lógico de assets que são um subconjunto do BaseAssetName. Por exemplo, se Bob tinha vários skins, esses skins ainda deveriam usar `Bob` como` BaseAssetName`, mas incluir uma `Variant` reconhecível. Um skin 'Evil' seria referido como `Bob_Evil` e um skin 'Retro' seria referido como` Bob_Retro`.

Para variações exclusivas, mas genéricas, de assets, `Variant` é um número de dois dígitos começando em` 01`. Por exemplo, se você tem um environment artist gerando rochas indefinidas, eles seriam chamados de `Rock_01`,` Rock_02`, `Rock_03`, etc. Exceto para raras exceções, você nunca deve exigir um número variante de três dígitos. Se você tiver mais de 100 assets, deve considerar organizá-los com BaseAssetName diferentes ou usando vários nomes de variantes.

Dependendo de como suas variações de assets são feitas, você pode encadear nomes de variações. Por exemplo, se você estiver criando assets de piso para um projeto Arch Viz, você deve usar o nome base `Flooring` com variações encadeadas como` Flooring_Marble_01`, `Flooring_Maple_01`,` Flooring_Tile_Squares_01`.

<a name="1.1-examples"></a>
#### 1.1 Exemplos

##### 1.1.1 Bob

| Asset Type              | Asset Name                                                 |
| ----------------------- | ---------------------------------------------------------- |
| Skeletal Mesh           | SK_Bob                                                     |
| Material                | M_Bob                                                      |
| Texture (Diffuse/Albedo)| T_Bob_D                                                    |
| Texture (Normal)        | T_Bob_N                                                    |
| Texture (Evil Diffuse)  | T_Bob_Evil_D                                               |

##### 1.1.2 Rocks

| Asset Type              | Asset Name                                                 |
| ----------------------- | ---------------------------------------------------------- |
| Static Mesh (01)        | S_Rock_01                                                  |
| Static Mesh (02)        | S_Rock_02                                                  |
| Static Mesh (03)        | S_Rock_03                                                  |
| Material                | M_Rock                                                     |
| Material Instance (Snow)| MI_Rock_Snow                                               |

<a name="asset-name-modifiers"></a>
<a name="1.2"></a>
### 1.2 Asset Name Modifiers

Ao nomear um asset, use essas tabelas para determinar o prefixo e o sufixo a serem usados com um asset [Base Asset Name](#base-asset-name).

#### Sections

> 1.2.1 [Most Common](#anc-common)

> 1.2.2 [Animations](#anc-animations)

> 1.2.3 [Artificial Intelligence](#anc-ai)

> 1.2.4 [Blueprints](#anc-bp)

> 1.2.5 [Materials](#anc-materials)

> 1.2.6 [Textures](#anc-textures)

> 1.2.7 [Miscellaneous](#anc-misc)

> 1.2.8 [Paper 2D](#anc-paper2d)

> 1.2.9 [Physics](#anc-physics)

> 1.2.10 [Sound](#anc-sounds)

> 1.2.11 [User Interface](#anc-ui)

> 1.2.12 [Effects](#anc-effects)

<a name="anc-common"></a>
<a name="1.2.1"></a>
#### 1.2.1 Most Common

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Level / Map             |            |            | [Deve estar em uma pasta chamada Maps.](#2.4) |
| Level (Persistent)      |            | _P         |                                  |
| Level (Audio)           |            | _Audio     |                                  |
| Level (Lighting)        |            | _Lighting  |                                  |
| Level (Geometry)        |            | _Geo       |                                  |
| Level (Gameplay)        |            | _Gameplay  |                                  |
| Blueprint               | BP_        |            |                                  |
| Material                | M_         |            |                                  |
| Static Mesh             | S_         |            | Muitos usam SM_. nós usamos S_.         |
| Skeletal Mesh           | SK_        |            |                                  |
| Texture                 | T_         | _?         | Veja [Textures](#anc-textures)    |
| Particle System         | PS_        |            |                                  |
| Widget Blueprint        | WBP_       |            |                                  |

<a name="anc-animations"></a>
<a name="1.2.2"></a>
#### 1.2.2 Animations

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Aim Offset              | AO_        |            |                                  |
| Aim Offset 1D           | AO_        |            |                                  |
| Animation Blueprint     | ABP_       |            |                                  |
| Animation Composite     | AC_        |            |                                  |
| Animation Montage       | AM_        |            |                                  |
| Animation Sequence      | A_         |            |                                  |
| Blend Space             | BS_        |            |                                  |
| Blend Space 1D          | BS_        |            |                                  |
| Level Sequence          | LS_        |            |                                  |
| Morph Target            | MT_        |            |                                  |
| Paper Flipbook          | PFB_       |            |                                  |
| Rig                     | Rig_       |            |                                  |
| Skeletal Mesh           | SK_        |            |                                  |
| Skeleton                | SKEL_      |            |                                  |

<a name="anc-ai"></a>
<a name="1.2.3"></a>
### 1.2.3 Artificial Intelligence

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| AI Controller           | AIC_       |            |                                  |
| Behavior Tree           | BT_        |            |                                  |
| Blackboard              | BB_        |            |                                  |
| Decorator               | BTDecorator_ |          |                                  |
| Service                 | BTService_ |            |                                  |
| Task                    | BTTask_    |            |                                  |
| Environment Query       | EQS_       |            |                                  |
| EnvQueryContext         | EQS_       | Context    |                                  |

<a name="anc-bp"></a>
<a name="1.2.4"></a>
### 1.2.4 Blueprints ![#](https://img.shields.io/badge/lint-supported-green.svg)

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Blueprint               | BP_        |            |                                  |
| Blueprint Component	  | BP_	       | Component  | Ex. BP_InventoryComponent        |
| Blueprint Function Library | BPFL_   |            |                                  |
| Blueprint Interface     | BPI_       |            |                                  |
| Blueprint Macro Library | BPML_      |            |                                  |
| Enumeration             | E          |            | Sem Underline.                   |
| Structure               | F or S     |            | Sem Underline.                   |
| Tutorial Blueprint      | TBP_       |            |                                  |
| Widget Blueprint        | WBP_       |            |                                  |

<a name="anc-materials"></a>
<a name="1.2.5"></a>
### 1.2.5 Materials

| Asset Type                    | Prefix     | Suffix     | Notes                            |
| ----------------------------- | ---------- | ---------- | -------------------------------- |
| Material                      | M_         |            |                                  |
| Material (Post Process)       | PP_        |            |                                  |
| Material Function             | MF_        |            |                                  |
| Material Instance             | MI_        |            |                                  |
| Material Parameter Collection | MPC_       |            |                                  |
| Subsurface Profile            | SP_        |            |                                  |
| Physical Materials            | PM_        |            |                                  |
| Decal                         | M_, MI_    | _Decal     |                                  |

<a name="anc-textures"></a>
<a name="1.2.6"></a>
### 1.2.6 Textures ![#](https://img.shields.io/badge/lint-supported-green.svg)

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Texture                 | T_         |            |                                  |
| Texture (Diffuse/Albedo/Base Color)| T_ | _D      |                                  |
| Texture (Normal)        | T_         | _N         |                                  |
| Texture (Roughness)     | T_         | _R         |                                  |
| Texture (Alpha/Opacity) | T_         | _A         |                                  |
| Texture (Ambient Occlusion) | T_     | _O         |                                  |
| Texture (Bump)          | T_         | _B         |                                  |
| Texture (Emissive)      | T_         | _E         |                                  |
| Texture (Mask)          | T_         | _M         |                                  |
| Texture (Specular)      | T_         | _S         |                                  |
| Texture (Metallic)      | T_         | _M         |                                  |
| Texture (Packed)        | T_         | _*         | Veja [packing](#anc-textures-packing). |
| Texture Cube            | TC_        |            |                                  |
| Media Texture           | MT_        |            |                                  |
| Render Target           | RT_        |            |                                  |
| Cube Render Target      | RTC_       |            |                                  |
| Texture Light Profile   | TLP        |            |                                  |

<a name="anc-textures-packing"></a>
<a name="1.2.6.1"></a>
#### 1.2.6.1 Texture Packing

É comum compactar várias camadas de dados de textura em uma textura. Um exemplo disso é empacotar Emissive, Roughness, Ambient Occlusion juntos como os canais Vermelho, Verde e Azul de uma textura, respectivamente. Para determinar o sufixo, basta empilhar as letras de sufixo fornecidas acima juntas, por exemplo, `_ERO`.

> É geralmente aceitável incluir uma camada Alpha / Opacity no canal Alpha de seu Diffuse / Albedo e como isso é uma prática comum, adicionar `A` ao sufixo` _D` é opcional.

Empacotar 4 canais de dados em uma textura (RGBA) não é recomendado, exceto para uma máscara Alpha / Opacity no canal Alpha do Diffuse / Albedo, pois uma textura com um canal alfa incorre em mais overhead do que uma sem.

<a name="anc-misc"></a>
<a name="1.2.7"></a>
### 1.2.7 Miscellaneous

| Asset Type                 | Prefix     | Suffix     | Notes                            |
| -------------------------- | ---------- | ---------- | -------------------------------- |
| Animated Vector Field      | VFA_       |            |                                  |
| Camera Anim                | CA_        |            |                                  |
| Color Curve                | Curve_     | _Color     |                                  |
| Curve Table                | Curve_     | _Table     |                                  |
| Data Asset                 | *_         |            | Prefix devem ser baseados na classe. |
| Data Table                 | DT_        |            |                                  |
| Float Curve                | Curve_     | _Float     |                                  |
| Foliage Type               | FT_        |            |                                  |
| Force Feedback Effect      | FFE_       |            |                                  |
| Landscape Grass Type       | LG_        |            |                                  |
| Landscape Layer            | LL_        |            |                                  |
| Matinee Data               | Matinee_   |            |                                  |
| Media Player               | MP_        |            |                                  |
| Object Library             | OL_        |            |                                  |
| Redirector                 |            |            | Eles devem ser corrigidos o mais rápido possível.   |
| Sprite Sheet               | SS_        |            |                                  |
| Static Vector Field        | VF_        |            |                                  |
| Substance Graph Instance   | SGI_       |            |                                  |
| Substance Instance Factory | SIF_       |            |                                  |
| Touch Interface Setup      | TI_        |            |                                  |
| Vector Curve               | Curve_     | _Vector    |                                  |

<a name="anc-paper2d"></a>
<a name="1.2.8"></a>
### 1.2.8 Paper 2D

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Paper Flipbook          | PFB_       |            |                                  |
| Sprite                  | SPR_       |            |                                  |
| Sprite Atlas Group      | SPRG_      |            |                                  |
| Tile Map                | TM_        |            |                                  |
| Tile Set                | TS_        |            |                                  |

<a name="anc-physics"></a>
<a name="1.2.9"></a>
### 1.2.9 Physics

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Physical Material       | PM_        |            |                                  |
| Physical Asset	  | PHYS_      |            |                                  |
| Destructible Mesh       | DM_        |            |                                  |

<a name="anc-sounds"></a>
<a name="1.2.10"></a>
### 1.2.10 Sounds

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Dialogue Voice          | DV_        |            |                                  |
| Dialogue Wave           | DW_        |            |                                  |
| Media Sound Wave        | MSW_       |            |                                  |
| Reverb Effect           | Reverb_    |            |                                  |
| Sound Attenuation       | ATT_       |            |                                  |
| Sound Class             |            |            | Sem prefix/suffix. Devem ser colocados em uma pasta chamada SoundClasses |
| Sound Concurrency       |            | _SC        | Devem ser nomeados com a SoundClass |
| Sound Cue               | A_         | _Cue       |                                  |
| Sound Mix               | Mix_       |            |                                  |
| Sound Wave              | A_         |            |                                  |

<a name="anc-ui"></a>
<a name="1.2.11"></a>
### 1.2.11 User Interface

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Font                    | Font_      |            |                                  |
| Slate Brush             | Brush_     |            |                                  |
| Slate Widget Style      | Style_     |            |                                  |
| Widget Blueprint        | WBP_       |            |                                  |

<a name="anc-effects"></a>
<a name="1.2.12"></a>
### 1.2.12 Effects

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Particle System         | PS_        |            |                                  |
| Material (Post Process) | PP_        |            |                                  |

**[⬆ Voltar ao topo](#table-of-contents)**


<a name="2"></a>
<a name="structure"></a>
## 2. Content Directory Structure

Tão importante quanto os nomes dos assets, o estilo da estrutura de diretório de um projeto deve ser considerado lei. As convenções de nomenclatura de assets e a estrutura do diretório de conteúdo andam de mãos dadas, e uma violação de qualquer uma delas causa um caos desnecessário.

Existem várias maneiras de definir o conteúdo de um projeto UE4. Nesse estilo, usaremos uma estrutura que depende mais dos recursos de filtragem e pesquisa do Content Browser para aqueles que trabalham com assets para encontrar assets de um tipo específico em vez de outra estrutura comum que agrupa tipos de assets com pastas.

> Se você estiver usando o prefixo [convenção de nomenclatura] (# 1.2), usar pastas para conter assets de tipos semelhantes, como `Meshes`, `Textures`, and `Materials` é uma prática redundante, pois os tipos de assets já estão classificados por prefixo, além de poder ser filtrado no Content Browser.

<a name="2e1"><a>
### 2e1 Example Project Content Structure
<pre>
|-- Content
    |-- <a href="#2.2">GenericShooter</a>
        |-- Art
        |   |-- Industrial
        |   |   |-- Ambient
        |   |   |-- Machinery
        |   |   |-- Pipes
        |   |-- Nature
        |   |   |-- Ambient
        |   |   |-- Foliage
        |   |   |-- Rocks
        |   |   |-- Trees
        |   |-- Office
        |-- Characters
        |   |-- Bob
        |   |-- Common
        |   |   |-- <a href="#2.7">Animations</a>
        |   |   |-- Audio
        |   |-- Jack
        |   |-- Steve
        |   |-- <a href="#2.1.3">Zoe</a>
        |-- <a href="#2.5">Core</a>
        |   |-- Characters
        |   |-- Engine
        |   |-- <a href="#2.1.2">GameModes</a>
        |   |-- Interactables
        |   |-- Pickups
        |   |-- Weapons
        |-- Effects
        |   |-- Electrical
        |   |-- Fire
        |   |-- Weather
        |-- <a href="#2.4">Maps</a>
        |   |-- Campaign1
        |   |-- Campaign2
        |-- <a href="#2.8">MaterialLibrary</a>
        |   |-- Debug
        |   |-- Metal
        |   |-- Paint
        |   |-- Utility
        |   |-- Weathering
        |-- Placeables
        |   |-- Pickups
        |-- Weapons
            |-- Common
            |-- Pistols
            |   |-- DesertEagle
            |   |-- RocketPistol
            |-- Rifles
</pre>

Os motivos para essa estrutura estão listados nas subseções a seguir.

### Seções

> 2.1 [Folder Names](#structure-folder-names)

> 2.2 [Top-Level Folders](#structure-top-level)

> 2.3 [Developer Folders](#structure-developers)

> 2.4 [Maps](#structure-maps)

> 2.5 [Core](#structure-core)

> 2.6 [`Assets` e `AssetTypes`](#structure-assettypes)

> 2.7 [Large Sets](#structure-large-sets)

> 2.8 [Material Library](#structure-material-library)


<a name="2.1"></a>
<a name="structure-folder-names"><a>
### 2.1 Folder Names
	
Essas são regras comuns para nomear qualquer pasta na estrutura de conteúdo.

<a name="2.1.1"></a>
#### 2.1.1 Always Use PascalCase[<sup>*</sup>](#terms-cases)

PascalCase se refere a iniciar um nome com uma letra maiúscula e, em vez de usar espaços, todas as palavras seguintes também começam com uma letra maiúscula. Por exemplo, `DesertEagle`,` RocketPistol` e `ASeriesOfWords`.

Veja [Cases](#terms-cases).

<a name="2.1.2"></a>
#### 2.1.2 Nunca Use Espaços

Reforçando [2.1.1] (# 2.1.1), nunca use espaços. Os espaços podem fazer com que várias ferramentas de engenharia e processos em lote falhem. Idealmente, a raiz do seu projeto também não contém espaços e está localizada em algum lugar como `D:\Project` em vez de `C:\Users\My Name\My Documents\Unreal Projects`.

<a name="2.1.3"></a>
#### 2.1.3 Nunca Use Caracteres Unicode e Outros Simbolos

Se um dos personagens do seu jogo se chama 'Zoë', o nome da pasta deve ser `Zoe`. Os caracteres Unicode podem ser piores do que [Espaços] (# 2.1.2) para a ferramenta de engenharia e algumas partes do UE4 também não suportam caracteres Unicode nos caminhos.

Relacionado a isso, se o seu projeto tiver [problemas inexplicáveis] (https://answers.unrealengine.com/questions/101207/undefined.html) e o nome de usuário do seu computador tiver um caractere Unicode (ou seja, seu nome é `Zoë`), qualquer projeto localizado na pasta `Meus Documentos` sofrerá com esse problema. Freqüentemente, simplesmente mover seu projeto para algo como `D:\Project` irá corrigir esses problemas misteriosos.

Usar outros caracteres fora de `az`,` AZ` e `0-9`, como` @ `,` -`, `_`,`, `,` * `e` # `também pode levar a problemas inesperados e difícil rastrear em outras plataformas, Source Control e ferramentas de engenharia mais fracas.

<a name="2.2"></a>
<a name="structure-top-level"><a>
### 2.2 Use Uma Pasta De Nível Superior Para Assets Específicos Do Projeto

Todos os assets de um projeto devem existir em uma pasta com o nome do projeto. Por exemplo, se o seu projeto se chama 'Generic Shooter', _todo_ o seu conteúdo deve existir em `Content/GenericShooter`.

> A pasta `Developers` não é para assets dos quais seu projeto depende e, portanto, não é específica do projeto. Consulte [Developer Folders] (# 2.3) para obter detalhes sobre isso.

Existem várias razões para esta abordagem.

<a name="2.2.1"></a>
#### 2.2.1 Sem Assets Globais

Freqüentemente, nos guias de estilo de código está escrito que você não deve poluir o namespace global e isso segue o mesmo princípio. Quando assets podem existir fora de uma pasta de projeto, geralmente se torna muito mais difícil impor um layout de estrutura estrito, pois assets que não estão em uma pasta encorajam o mau comportamento de não ter que organizar assets.

Todo asset deve ter um propósito, caso contrário, ele não pertence a um projeto. Se um asset é um teste experimental e não deve ser usado pelo projeto, ele deve ser colocado em uma pasta [`Developer`] (# 2.3).

<a name="2.2.2"></a>
#### 2.2.2 Reduzir Conflitos De Migração

Ao trabalhar em vários projetos, é comum que uma equipe copie assets de um projeto para outro, caso tenham feito algo útil para ambos. Quando isso ocorre, a maneira mais fácil de realizar a cópia é usar a funcionalidade Migrate do Content Browser, pois ela copiará não apenas o asset selecionado, mas todas as suas dependências.

Essas dependências podem facilmente causar problemas. Se os assets de dois projetos não tiverem uma pasta de nível superior e acontecerem de terem assets com nomes semelhantes ou já migrados anteriormente, uma nova migração pode apagar acidentalmente quaisquer alterações nos assets existentes.

Esse também é o principal motivo pelo qual a equipe do Marketplace da Epic aplica a mesma política para os assets enviados.

Após uma migração, a fusão segura de assets pode ser feita usando a ferramenta 'Replace References' no Content Browser com a clareza adicional de assets que não pertencem à pasta de nível superior de um projeto e estão claramente pendentes de uma fusão. Depois que os ativos são mesclados e totalmente migrados, não deve haver outra pasta de nível superior em sua árvore de conteúdo. Esse método é _100% _ garantido para tornar todas as migrações que ocorrerem completamente seguras.

<a name="2.2.2.1"></a>
##### 2.2.2.1 Exemplo: Master Material

Por exemplo, digamos que você criou um Master Material em um projeto que gostaria de usar em outro projeto, então migrou esse asset. Se este asset não estiver em uma pasta de nível superior, pode ter um nome como `Content/MaterialLibrary/M_Master`. Se o projeto de destino ainda não tiver um Master Material, isso deve funcionar sem problemas.

Conforme o trabalho em um ou ambos os projetos progride, seus respectivos Master Materials podem mudar para serem adaptados para seus projetos específicos devido ao curso de desenvolvimento normal.

O problema surge quando, por exemplo, um artista para um projeto criou um bom conjunto modular genérico de static meshs e alguém deseja incluir esse conjunto de static meshs no segundo projeto. Se o artista que criou os recursos usou material instances com base em `Content/MaterialLibrary/M_Master` conforme instruído, quando uma migração é realizada, há uma grande chance de conflito para o recurso `Content/MaterialLibrary/M_Master` migrado anteriormente .

Esse problema pode ser difícil de prever e de explicar. A pessoa que migra as malhas estáticas pode não ser a mesma pessoa que está familiarizada com o desenvolvimento de ambos os master materials do projeto e pode nem mesmo estar ciente de que as static meshs em questão dependem de material instances que, então, dependem do master material. A ferramenta Migrate requer que toda a cadeia de dependências funcione, portanto, será forçada a pegar `Content/MaterialLibrary/M_Master` ao copiar esses assets para outro projeto e sobrescrever o asset existente.

É neste ponto que se os master material para ambos os projetos forem incompatíveis de _qualquer maneira_, você corre o risco de quebrar possivelmente toda a biblioteca de materiais de um projeto, bem como quaisquer outras dependências que já possam ter sido migradas, simplesmente porque os assets não foram armazenados em uma pasta de nível superior. A simples migração de static meshs agora se torna uma tarefa muito díficil de se resolver.

<a name="2.2.3"></a>
#### 2.2.3 Samples, Templates, e Conteúdo dop Marketplace São Livres de Riscos

Uma extensão para [2.2.2] (# 2.2.2), se um membro da equipe decidir adicionar conteúdo de amostra, arquivos de templates ou assets que comprou no marketplace, isso é garantido, desde que a pasta de nível superior do seu projeto seja exclusivamente nomeado, esses novos ativos não interferirão em seu projeto.

Você não pode confiar que o conteúdo do marketplace está em total conformidade com a [regra de pasta de nível superior] (# 2.2). Existem muitos ativos que têm a maior parte de seu conteúdo em uma pasta de nível superior, mas também possuem conteúdo da Epic possivelmente modificado, bem como arquivos de mapas poluindo a pasta global `Content`.

Ao aderir a [2.2] (# 2.2), o pior conflito de marketplace que você pode ter é se dois ativos do marketplace tiverem o mesmo conteúdo da Epic. Se todos os seus recursos estiverem em uma pasta específica do projeto, incluindo conteúdo de amostra que você pode ter movido para a pasta, seu projeto nunca será interrompido.

#### 2.2.4 DLC, Sub-Projetos, e Patches São Facilmente Mantidos

Se o seu projeto planeja liberar DLC ou tem vários sub-projetos associados a ele que podem ser migrados ou simplesmente não foi feito o cooking em uma build, os assets relacionados a esses projetos devem ter sua própria pasta de conteúdo de nível superior separada. Isso torna muito mais fácil fazer o cook do DLC separado do conteúdo do projeto principal. Os sub-projetos também podem ser migrados para dentro e para fora com o mínimo de esforço. Se você precisar alterar um material de um asset ou adicionar algum comportamento de substituição de assets muito específico em um patch, pode facilmente colocar essas alterações em uma pasta de patch e trabalhar com segurança sem a chance de quebrar o projeto principal.

<a name="2.3"></a>
<a name="structure-developers"></a>
### 2.3 Use A Pasta De Desenvolvedores Para Testes Locais

Durante o desenvolvimento de um projeto, é muito comum que os membros da equipe tenham uma espécie de 'sandbox' onde podem experimentar livremente sem arriscar o projeto principal. Como esse trabalho pode estar em andamento, esses membros da equipe podem desejar colocar seus assets em um servidor Source Control do projeto. Nem todas as equipes exigem o uso de pastas de desenvolvedor, mas aquelas que as usam costumam ter um problema comum com ativos submetidos ao servidor Source Control.

É muito fácil para um membro da equipe usar acidentalmente assets que não estão prontos para uso, o que causará problemas quando esses assets forem removidos. Por exemplo, um artista pode estar iterando em um conjunto modular de static meshs e ainda trabalhando para obter o tamanho e o encaixe da grade corretos. Se um level designer vir esses assets na pasta principal do projeto, ele pode usá-los em um nível sem saber que podem estar sujeitos a mudanças e / ou remoções. Isso causa uma grande quantidade de retrabalho de todos na equipe para resolver.

Se esses ativos modulares fossem colocados em uma pasta de desenvolvedor, o Level Designer nunca deveria ter um motivo para usá-los e todo o problema nunca aconteceria. O Navegador de conteúdo tem opções de exibição específicas que ocultam as pastas do desenvolvedor (elas ficam ocultas por padrão), tornando impossível o uso acidental de ativos do desenvolvedor em uso normal.

Depois que os recursos estão prontos para uso, o artista simplesmente precisa mover os recursos para a pasta específica do projeto e corrigir os redirecionadores. Isso é essencialmente 'promover' os ativos do experimental para a produção.

<a name="2.4"></a>
<a name="structure-maps"></a>
### 2.4 All Map[<sup>*</sup>](#terms-level-map) Files Belong In A Folder Called Maps ![#](https://img.shields.io/badge/lint-supported-green.svg)

Map files are incredibly special and it is common for every project to have its own map naming system, especially if they work with sub-levels or streaming levels. No matter what system of map organization is in place for the specific project, all levels should belong in `/Content/Project/Maps`.

Being able to tell someone to open a specific map without having to explain where it is is a great time saver and general 'quality of life' improvement. It is common for levels to be within sub-folders of `Maps`, such as `Maps/Campaign1/` or `Maps/Arenas`, but the most important thing here is that they all exist within `/Content/Project/Maps`.

This also simplifies the job of cooking for engineers. Wrangling levels for a build process can be extremely frustrating if they have to dig through arbitrary folders for them. If a team's maps are all in one place, it is much harder to accidentally not cook a map in a build. It also simplifies lighting build scripts as well as QA processes.

<a name="2.5"></a>
<a name="structure-core"></a>
### 2.5 Use A `Core` Folder For Critical Blueprints And Other Assets ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

Use `/Content/Project/Core` folder for assets that are absolutely fundamental to a project's workings. For example, base `GameMode`, `Character`, `PlayerController`, `GameState`, `PlayerState`, and related Blueprints should live here.

This creates a very clear "don't touch these" message for other team members. Non-engineers should have very little reason to enter the `Core` folder. Following good code structure style, designers should be making their gameplay tweaks in child classes that expose functionality. World builders should be using prefab Blueprints in designated folders instead of potentially abusing base classes.

For example, if your project requires pickups that can be placed in a level, there should exist a base Pickup class in `Core/Pickups` that defines base behavior for a pickup. Specific pickups such as a Health or Ammo should exist in a folder such as `/Content/Project/Placeables/Pickups/`. Game designers can define and tweak pickups in this folder however they please, but they should not touch `Core/Pickups` as they may unintentionally break pickups project-wide.

<a name="2.6"></a>
<a name="structure-assettypes"></a>
### 2.6 Do Not Create Folders Called `Assets` or `AssetTypes` ![#](https://img.shields.io/badge/lint-supported-green.svg)

<a name="2.6.1"></a>
#### 2.6.1 Creating a folder named `Assets` is redundant. ![#](https://img.shields.io/badge/lint-supported-green.svg)

All assets are assets.

<a name="2.6.2"></a>
#### 2.6.2 Creating a folder named `Meshes`, `Textures`, or `Materials` is redundant. ![#](https://img.shields.io/badge/lint-supported-green.svg)

All asset names are named with their asset type in mind. These folders offer only redundant information and the use of these folders can easily be replaced with the robust and easy to use filtering system the Content Browser provides.

Want to view only static mesh in `Environment/Rocks/`? Simply turn on the Static Mesh filter. If all assets are named correctly, they will also be sorted in alphabetical order regardless of prefixes. Want to view both static meshes and skeletal meshes? Simply turn on both filters. This eliminates the need to potentially have to `Control-Click` select two folders in the Content Browser's tree view.

> This also extends the full path name of an asset for very little benefit. The `S_` prefix for a static mesh is only two characters, whereas `Meshes/` is seven characters.

Not doing this also prevents the inevitability of someone putting a static mesh or a texture in a `Materials` folder.

<a name="2.7"></a>
<a name="structure-large-sets"></a>
### 2.7 Very Large Asset Sets Get Their Own Folder Layout ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

This can be seen as a pseudo-exception to [2.6](#2.6).

There are certain asset types that have a huge volume of related files where each asset has a unique purpose. The two most common are Animation and Audio assets. If you find yourself having 15+ of these assets that belong together, they should be together.

For example, animations that are shared across multiple characters should lay in `Characters/Common/Animations` and may have sub-folders such as `Locomotion` or `Cinematic`.

> This does not apply to assets like textures and materials. It is common for a `Rocks` folder to have a large amount of textures if there are a large amount of rocks, however these textures are generally only related to a few specific rocks and should be named appropriately. Even if these textures are part of a [Material Library](#2.8).

<a name="2.8"></a>
<a name="structure-material-library"></a>
### 2.8 `MaterialLibrary` ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

If your project makes use of master materials, layered materials, or any form of reusable materials or textures that do not belong to any subset of assets, these assets should be located in `Content/Project/MaterialLibrary`.

This way all 'global' materials have a place to live and are easily located.

> This also makes it incredibly easy to enforce a 'use material instances only' policy within a project. If all artists and assets should be using material instances, then the only regular material assets that should exist are within this folder. You can easily verify this by searching for base materials in any folder that isn't the `MaterialLibrary`.

The `MaterialLibrary` doesn't have to consist of purely materials. Shared utility textures, material functions, and other things of this nature should be stored here as well within folders that designate their intended purpose. For example, generic noise textures should be located in `MaterialLibrary/Utility`.

Any testing or debug materials should be within `MaterialLibrary/Debug`. This allows debug materials to be easily stripped from a project before shipping and makes it incredibly apparent if production assets are using them if reference errors are shown.

<a name="2.9"></a>
<a name="structure-no-empty-folders"></a>
### 2.9 No Empty Folders ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

There simply shouldn't be any empty folders. They clutter the content browser.

If you find that the content browser has an empty folder you can't delete, you should perform the following:
1. Be sure you're using source control.
1. Immediately run Fix Up Redirectors on your project.
1. Navigate to the folder on-disk and delete the assets inside.
1. Close the editor.
1. Make sure your source control state is in sync (i.e. if using Perforce, run a Reconcile Offline Work on your content directory)
1. Open the editor. Confirm everything still works as expected. If it doesn't, revert, figure out what went wrong, and try again.
1. Ensure the folder is now gone.
1. Submit changes to source control.

**[⬆ Back to Top](#table-of-contents)**


<a name="3"></a>
<a name="bp"></a>
## 3. Blueprints ![#](https://img.shields.io/badge/lint-partial_support-yellow.svg)

This section will focus on Blueprint classes and their internals. When possible, style rules conform to [Epic's Coding Standard](https://docs.unrealengine.com/latest/INT/Programming/Development/CodingStandard).

Remember: Blueprinting badly bears blunders, beware! (Phrase by [KorkuVeren](http://github.com/KorkuVeren))

### Sections

> 3.1 [Compiling](#bp-compiling)

> 3.2 [Variables](#bp-vars)

> 3.3 [Functions](#bp-functions)

> 3.4 [Graphs](#bp-graphs)

<a name="3.1"></a>
<a name="bp-compiling"></a>
### 3.1 Compiling ![#](https://img.shields.io/badge/lint-supported-green.svg)

All blueprints should compile with zero warnings and zero errors. You should fix blueprint warnings and errors immediately as they can quickly cascade into very scary unexpected behavior.

Do *not* submit broken blueprints to source control. If you must store them on source control, shelve them instead.

Broken blueprints can cause problems that manifest in other ways, such as broken references, unexpected behavior, cooking failures, and frequent unneeded recompilation. A broken blueprint has the power to break your entire game.

<a name="3.2"></a>
<a name="bp-vars"></a>
### 3.2 Variables ![#](https://img.shields.io/badge/lint-partial_support-yellow.svg)

The words `variable` and `property` may be used interchangeably.

#### Sections

> 3.2.1 [Naming](#bp-vars)

> 3.2.2 [Editable](#bp-vars-editable)

> 3.2.3 [Categories](#bp-vars-categories)

> 3.2.4 [Access](#bp-vars-access)

> 3.2.5 [Advanced](#bp-vars-advanced)

> 3.2.6 [Transient](#bp-vars-transient)

> 3.2.7 [Config](#bp-vars-config)

<a name="3.2.1"></a>
<a name="bp-var-naming"></a>
#### 3.2.1 Naming ![#](https://img.shields.io/badge/lint-partial_support-yellow.svg)

<a name="3.2.1.1"></a>
<a name="bp-var-naming-nouns"></a>
##### 3.2.1.1 Nouns ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

All non-boolean variable names must be clear, unambiguous, and descriptive nouns.

<a name="3.2.1.2"></a>
<a name="bp-var-naming-case"></a>
##### 3.2.1.2 PascalCase ![#](https://img.shields.io/badge/lint-supported-green.svg)

All non-boolean variables should be in the form of [PascalCase](#terms-cases).

<a name="3.2.1.2e"></a>
###### 3.2.1.2e Examples:

* `Score`
* `Kills`
* `TargetPlayer`
* `Range`
* `CrosshairColor`
* `AbilityID`

<a name="3.2.1.3"></a>
<a name="bp-var-bool-prefix"></a>
##### 3.2.1.3 Boolean `b` Prefix ![#](https://img.shields.io/badge/lint-supported-green.svg)

All booleans should be named in PascalCase but prefixed with a lowercase `b`.

Example: Use `bDead` and `bEvil`, **not** `Dead` and `Evil`.

UE4 Blueprint editors know not to include the `b` in user-friendly displays of the variable.

<a name="3.2.1.4"></a>
<a name="bp-var-bool-names"></a>
##### 3.2.1.4 Boolean Names ![#](https://img.shields.io/badge/lint-partial_support-yellow.svg)

<a name="3.2.1.4.1"></a>
###### 3.2.1.4.1 General And Independent State Information ![#](https://img.shields.io/badge/lint-supported-green.svg)

All booleans should be named as descriptive adjectives when possible if representing general information. Do not include words that phrase the variable as a question, such as `Is`. This is reserved for functions.

Example: Use `bDead` and `bHostile` **not** `bIsDead` and `bIsHostile`.

Try to not use verbs such as `bRunning`. Verbs tend to lead to complex states.

<a name="3.2.1.4.2"></a>
###### 3.2.1.4.2 Complex States ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

Do not to use booleans to represent complex and/or dependent states. This makes state adding and removing complex and no longer easily readable. Use an enumeration instead.

Example: When defining a weapon, do **not** use `bReloading` and `bEquipping` if a weapon can't be both reloading and equipping. Define an enumeration named `EWeaponState` and use a variable with this type named `WeaponState` instead. This makes it far easier to add new states to weapons.

Example: Do **not** use `bRunning` if you also need `bWalking` or `bSprinting`. This should be defined as an enumeration with clearly defined state names.

<a name="3.2.1.5"></a>
<a name="bp-vars-naming-context"></a>
##### 3.2.1.5 Considered Context ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

All variable names must not be redundant with their context as all variable references in Blueprint will always have context.

<a name="3.2.1.5e"></a>
###### 3.2.1.5e Examples:

Consider a Blueprint called `BP_PlayerCharacter`.

**Bad**

* `PlayerScore`
* `PlayerKills`
* `MyTargetPlayer`
* `MyCharacterName`
* `CharacterSkills`
* `ChosenCharacterSkin`

All of these variables are named redundantly. It is implied that the variable is representative of the `BP_PlayerCharacter` it belongs to because it is `BP_PlayerCharacter` that is defining these variables.

**Good**

* `Score`
* `Kills`
* `TargetPlayer`
* `Name`
* `Skills`
* `Skin`

<a name="3.2.1.6"></a>
<a name="bp-vars-naming-atomic"></a>
##### 3.2.1.6 Do _Not_ Include Atomic Type Names ![#](https://img.shields.io/badge/lint-supported-green.svg)

Atomic or primitive variables are variables that represent data in their simplest form, such as booleans, integers, floats, and enumerations.

Strings and vectors are considered atomic in terms of style when working with Blueprints, however they are technically not atomic.

> While vectors consist of three floats, vectors are often able to be manipulated as a whole, same with rotators.

> Do _not_ consider Text variables as atomic, they are secretly hiding localization functionality. The atomic type of a string of characters is `String`, not `Text`.

Atomic variables should not have their type name in their name.

Example: Use `Score`, `Kills`, and `Description` **not** `ScoreFloat`, `FloatKills`, `DescriptionString`.

The only exception to this rule is when a variable represents 'a number of' something to be counted _and_ when using a name without a variable type is not easy to read.

Example: A fence generator needs to generate X number of posts. Store X in `NumPosts` or `PostsCount` instead of `Posts` as `Posts` may potentially read as an Array of a variable type named `Post`.

<a name="3.2.1.7"></a>
<a name="bp-vars-naming-complex"></a>
##### 3.2.1.7 Do Include Non-Atomic Type Names ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

Non-atomic or complex variables are variables that represent data as a collection of atomic variables. Structs, Classes, Interfaces, and primitives with hidden behavior such as `Text` and `Name` all qualify under this rule.

> While an Array of an atomic variable type is a list of variables, Arrays do not change the 'atomicness' of a variable type.

These variables should include their type name while still considering their context.

If a class owns an instance of a complex variable, i.e. if a `BP_PlayerCharacter` owns a `BP_Hat`, it should be stored as the variable type as without any name modifications.

Example: Use `Hat`, `Flag`, and `Ability` **not** `MyHat`, `MyFlag`, and `PlayerAbility`.

If a class does not own the value a complex variable represents, you should use a noun along with the variable type.

Example: If a `BP_Turret` has the ability to target a `BP_PlayerCharacter`, it should store its target as `TargetPlayer` as when in the context of `BP_Turret` it should be clear that it is a reference to another complex variable type that it does not own.


<a name="3.2.1.8"></a>
<a name="bp-vars-naming-arrays"></a>
##### 3.2.1.8 Arrays ![#](https://img.shields.io/badge/lint-partial_support-yellow.svg)

Arrays follow the same naming rules as above, but should be named as a plural noun.

Example: Use `Targets`, `Hats`, and `EnemyPlayers`, **not** `TargetList`, `HatArray`, `EnemyPlayerArray`.


<a name="3.2.2"></a>
<a name="bp-vars-editable"></a>
#### 3.2.2 Editable Variables ![#](https://img.shields.io/badge/lint-partial_support-yellow.svg)

All variables that are safe to change the value of in order to configure behavior of a blueprint should be marked as `Editable`.

Conversely, all variables that are not safe to change or should not be exposed to designers should _not_ be marked as editable, unless for engineering reasons the variable must be marked as `Expose On Spawn`.

Do not arbitrarily mark variables as `Editable`.

<a name="3.2.2.1"></a>
<a name="bp-vars-editable-tooltips"></a>
##### 3.2.2.1 Tooltips ![#](https://img.shields.io/badge/lint-supported-green.svg)

All `Editable` variables, including those marked editable just so they can be marked as `Expose On Spawn`, should have a description in their `Tooltip` fields that explains how changing this value affects the behavior of the blueprint.

<a name="3.2.2.2"></a>
<a name="bp-vars-editable-ranges"></a>
##### 3.2.2.2 Slider And Value Ranges ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

All `Editable` variables should make use of slider and value ranges if there is ever a value that a variable should _not_ be set to.

Example: A blueprint that generates fence posts might have an editable variable named `PostsCount` and a value of -1 would not make any sense. Use the range fields to mark 0 as a minimum.

If an editable variable is used in a Construction Script, it should have a reasonable Slider Range defined so that someone can not accidentally assign it a large value that could crash the editor.

A Value Range only needs to be defined if the bounds of a value are known. While a Slider Range prevents accidental large number inputs, an undefined Value Range allows a user to specify a value outside the Slider Range that may be considered 'dangerous' but still valid.

<a name="3.2.3"></a>
<a name="bp-vars-categories"></a>
#### 3.2.3 Categories ![#](https://img.shields.io/badge/lint-supported-green.svg)

If a class has only a small number of variables, categories are not required.

If a class has a moderate amount of variables (5-10), all `Editable` variables should have a non-default category assigned. A common category is `Config`.

If a class has a large amount of variables, all `Editable` variables should be categorized into sub-categories using the category `Config` as the base category. Non-editable variables should be categorized into descriptive categories describing their usage. 

> You can define sub-categories by using the pipe character `|`, i.e. `Config | Animations`.

Example: A weapon class set of variables might be organized as:

	|-- Config
	|	|-- Animations
	|	|-- Effects
	|	|-- Audio
	|	|-- Recoil
	|	|-- Timings
	|-- Animations
	|-- State
	|-- Visuals

<a name="3.2.4"></a>
<a name="bp-vars-access"></a>
#### 3.2.4 Variable Access Level ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

In C++, variables have a concept of access level. Public means any code outside the class can access the variable. Protected means only the class and any child classes can access this variable internally. Private means only this class and no child classes can access this variable.

Blueprints do not have a defined concept of protected access currently.

Treat `Editable` variables as public variables. Treat non-editable variables as protected variables.

<a name="3.2.4.1"></a>
<a name="bp-vars-access-private"></a>
##### 3.2.4.1 Private Variables ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

Unless it is known that a variable should only be accessed within the class it is defined and never a child class, do not mark variables as private. Until variables are able to be marked `protected`, reserve private for when you absolutely know you want to restrict child class usage.

<a name="3.2.5"></a>
<a name="bp-vars-advanced"></a>
#### 3.2.5 Advanced Display ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

If a variable should be editable but often untouched, mark it as `Advanced Display`. This makes the variable hidden unless the advanced display arrow is clicked.

To find the `Advanced Display` option, it is listed as an advanced displayed variable in the variable details list.

<a name="3.2.6"></a>
<a name="bp-vars-transient"></a>
#### 3.2.6 Transient Variables ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

Transient variables are variables that do not need to have their value saved and loaded and have an initial value of zero or null. This is useful for references to other objects and actors who's value isn't known until run-time. This prevents the editor from ever saving a reference to it, and speeds up saving and loading of the blueprint class.

Because of this, all transient variables should always be initialized as zero or null. To do otherwise would result in hard to debug errors.

<a name="3.2.7"></a>
<a name="bp-vars-config"></a>
#### 3.2.8 Config Variables ![#](https://img.shields.io/badge/lint-supported-green.svg)

Do not use the `Config Variable` flag. This makes it harder for designers to control blueprint behavior. Config variables should only be used in C++ for rarely changed variables. Think of them as `Advanced Advanced Display` variables.

<a name="3.3"></a>
<a name="bp-functions"></a>
### 3.3 Functions, Events, and Event Dispatchers ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

This section describes how you should author functions, events, and event dispatchers. Everything that applies to functions also applies to events, unless otherwise noted.

<a name="3.3.1"></a>
<a name="bp-funcs-naming"></a>
#### 3.3.1 Function Naming ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

The naming of functions, events, and event dispatchers is critically important. Based on the name alone, certain assumptions can be made about functions. For example:

* Is it a pure function?
* Is it fetching state information?
* Is it a handler?
* Is it an RPC?
* What is its purpose?

These questions and more can all be answered when functions are named appropriately.

<a name="3.3.1.1"></a>
<a name="bp-funcs-naming-verbs"></a>
#### 3.3.1.1 All Functions Should Be Verbs ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

All functions and events perform some form of action, whether its getting info, calculating data, or causing something to explode. Therefore, all functions should all start with verbs. They should be worded in the present tense whenever possible. They should also have some context as to what they are doing.

`OnRep` functions, event handlers, and event dispatchers are an exception to this rule.

Good examples:

* `Fire` - Good example if in a Character / Weapon class, as it has context. Bad if in a Barrel / Grass / any ambiguous class.
* `Jump` - Good example if in a Character class, otherwise, needs context.
* `Explode`
* `ReceiveMessage`
* `SortPlayerArray`
* `GetArmOffset`
* `GetCoordinates`
* `UpdateTransforms`
* `EnableBigHeadMode`
* `IsEnemy` - ["Is" is a verb.](http://writingexplained.org/is-is-a-verb)

Bad examples:

* `Dead` - Is Dead? Will deaden?
* `Rock`
* `ProcessData` - Ambiguous, these words mean nothing.
* `PlayerState` - Nouns are ambiguous.
* `Color` - Verb with no context, or ambiguous noun.

<a name="3.3.1.2"></a>
<a name="bp-funcs-naming-onrep"></a>
#### 3.3.1.2 Property RepNotify Functions Always `OnRep_Variable` ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

All functions for replicated with notification variables should have the form `OnRep_Variable`. This is forced by the Blueprint editor. If you are writing a C++ `OnRep` function however, it should also follow this convention when exposing it to Blueprints.

<a name="3.3.1.3"></a>
<a name="bp-funcs-naming-bool"></a>
#### 3.3.1.3 Info Functions Returning Bool Should Ask Questions ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

When writing a function that does not change the state of or modify any object and is purely for getting information, state, or computing a yes/no value, it should ask a question. This should also follow [the verb rule](#bp-funcs-naming-verbs).

This is extremely important as if a question is not asked, it may be assumed that the function performs an action and is returning whether that action succeeded.

Good examples:

* `IsDead`
* `IsOnFire`
* `IsAlive`
* `IsSpeaking`
* `IsHavingAnExistentialCrisis`
* `IsVisible`
* `HasWeapon` - ["Has" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)
* `WasCharging` - ["Was" is past-tense of "be".](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html) Use "was" when referring to 'previous frame' or 'previous state'.
* `CanReload` - ["Can" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)

Bad examples:

* `Fire` - Is on fire? Will fire? Do fire?
* `OnFire` - Can be confused with event dispatcher for firing.
* `Dead` - Is dead? Will deaden?
* `Visibility` - Is visible? Set visibility? A description of flying conditions?

<a name="3.3.1.4"></a>
<a name="bp-funcs-naming-eventhandlers"></a>
#### 3.3.1.4 Event Handlers and Dispatchers Should Start With `On` ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

Any function that handles an event or dispatches an event should start with `On` and continue to follow [the verb rule](#bp-funcs-naming-verbs). The verb may move to the end however if past-tense reads better.

[Collocations](http://dictionary.cambridge.org/us/grammar/british-grammar/about-words-clauses-and-sentences/collocation) of the word `On` are exempt from following the verb rule.

`Handle` is not allowed. It is 'Unreal' to use `On` instead of `Handle`, while other frameworks may prefer to use `Handle` instead of `On`.

Good examples:

* `OnDeath` - Common collocation in games
* `OnPickup`
* `OnReceiveMessage`
* `OnMessageRecieved`
* `OnTargetChanged`
* `OnClick`
* `OnLeave`

Bad examples:

* `OnData`
* `OnTarget`
* `HandleMessage`
* `HandleDeath`

<a name="3.3.1.5"></a>
<a name="bp-funcs-naming-rpcs"></a>
#### 3.3.1.5 Remote Procedure Calls Should Be Prefixed With Target ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

Any time an RPC is created, it should be prefixed with either `Server`, `Client`, or `Multicast`. No exceptions.

After the prefix, follow all other rules regarding function naming.

Good examples:

* `ServerFireWeapon`
* `ClientNotifyDeath`
* `MulticastSpawnTracerEffect`

Bad examples:

* `FireWeapon` - Does not indicate its an RPC of some kind.
* `ServerClientBroadcast` - Confusing.
* `AllNotifyDeath` - Use `Multicast`, never `All`.
* `ClientWeapon` - No verb, ambiguous.


<a name="3.3.2"></a>
<a name="bp-funcs-return"></a>
#### 3.3.2 All Functions Must Have Return Nodes ![#](https://img.shields.io/badge/lint-supported-green.svg)

All functions must have return nodes, no exceptions.

Return nodes explicitly note that a function has finished its execution. In a world where blueprints can be filled with `Sequence`, `ForLoopWithBreak`, and backwards reroute nodes, explicit execution flow is important for readability, maintenance, and easier debugging.

The Blueprint compiler is able to follow the flow of execution and will warn you if there is a branch of your code with an unhandled return or bad flow if you use return nodes.

In situations like where a programmer may add a pin to a Sequence node or add logic after a for loop completes but the loop iteration might return early, this can often result in an accidental error in code flow. The warnings the Blueprint compiler will alert everyone of these issues immediately.

<a name="3.3.3"></a>
<a name="bp-graphs-funcs-node-limit"></a>
#### 3.3.3 No Function Should Have More Than 50 Nodes ![#](https://img.shields.io/badge/lint-supported-green.svg)

Simply, no function should have more than 50 nodes. Any function this big should be broken down into smaller functions for readability and ease of maintenance.

The following nodes are not counted as they are deemed to not increase function complexity:

* Comment
* Route
* Cast
* Getting a Variable
* Breaking a Struct
* Function Entry
* Self

<a name="3.3.4"></a>
<a name="bp-graphs-funcs-description"></a>
#### 3.3.4 All Public Functions Should Have A Description ![#](https://img.shields.io/badge/lint-supported-green.svg)

This rule applies more to public facing or marketplace blueprints, so that others can more easily navigate and consume your blueprint API.

Simply, any function that has an access specificer of Public should have its description filled out. 

<a name="3.3.5"></a>
<a name="bp-graphs-funcs-plugin-category"></a>
#### 3.3.5 All Custom Static Plugin `BlueprintCallable` Functions Must Be Categorized By Plugin Name ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

If your project includes a plugin that defines `static` `BlueprintCallable` functions, they should have their category set to the plugin's name or a subset category of the plugin's name.

For example, `Zed Camera Interface` or `Zed Camera Interface | Image Capturing`.

<a name="3.4"></a>
<a name="bp-graphs"></a>
### 3.4 Blueprint Graphs ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

This section covers things that apply to all Blueprint graphs.

<a name="3.4.1"></a>
<a name="bp-graphs-spaghetti"></a>
#### 3.4.1 No Spaghetti ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

Wires should have clear beginnings and ends. You should never have to mentally untangle wires to make sense of a graph. Many of the following sections are dedicated to reducing spaghetti.

<a name="3.4.2"></a>
<a name="bp-graphs-align-wires"></a>
#### 3.4.2 Align Wires Not Nodes ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

Always align wires, not nodes. You can't always control the size and pin location on a node, but you can always control the location of a node and thus control the wires. Straight wires provide clear linear flow. Wiggly wires wear wits wickedly. You can straighten wires by using the Straighten Connections command with BP nodes selected. Hotkey: Q

Good example: The tops of the nodes are staggered to keep a perfectly straight white exec line.
![Aligned By Wires](https://github.com/allar/ue4-style-guide/raw/master/images/bp-graphs-align-wires-good.png "Aligned By Wires")

Bad Example: The tops of the nodes are aligned creating a wiggly white exec line.
![Bad](https://github.com/allar/ue4-style-guide/raw/master/images/bp-graphs-align-wires-bad.png "Wiggly")

Acceptable Example: Certain nodes might not cooperate no matter how you use the alignment tools. In this situation, try to minimize the wiggle by bringing the node in closer.
![Acceptable](https://github.com/allar/ue4-style-guide/raw/master/images/bp-graphs-align-wires-acceptable.png "Acceptable")

<a name="3.4.3"></a>
<a name="bp-graphs-exec-first-class"></a>
#### 3.4.3 White Exec Lines Are Top Priority ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

If you ever have to decide between straightening a linear white exec line or straightening data lines of some kind, always straighten the white exec line.

<a name="3.4.4"></a>
<a name="bp-graphs-block-comments"></a>
#### 3.4.4 Graphs Should Be Reasonably Commented ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

Blocks of nodes should be wrapped in comments that describe their higher-level behavior. While every function should be well named so that each individual node is easily readable and understandable, groups of nodes contributing to a purpose should have their purpose described in a comment block. If a function does not have many blocks of nodes and its clear that the nodes are serving a direct purpose in the function's goal, then they do not need to be commented as the function name and  description should suffice.

<a name="3.4.5"></a>
<a name="bp-graphs-cast-error-handling"></a>
#### 3.4.5 Graphs Should Handle Casting Errors Where Appropriate ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

If a function or event assumes that a cast always succeeds, it should appropriately report a failure in logic if the cast fails. This lets others know why something that is 'supposed to work' doesn't. A function should also attempt a graceful recover after a failed cast if it's known that the reference being casted could ever fail to be casted.

This does not mean every cast node should have its failure handled. In many cases, especially events regarding things like collisions, it is expected that execution flow terminates on a failed cast quietly.

<a name="3.4.6"></a>
<a name="bp-graphs-dangling-nodes"></a>
#### 3.4.6 Graphs Should Not Have Any Dangling / Loose / Dead Nodes ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

All nodes in all blueprint graphs must have a purpose. You should not leave dangling blueprint nodes around that have no purpose or are not executed.

**[⬆ Back to Top](#table-of-contents)**


<a name="4"></a>
<a name="Static Meshes"></a>
<a name="s"></a>
## 4. Static Meshes ![#](https://img.shields.io/badge/lint-partial_support-yellow.svg)

This section will focus on Static Mesh assets and their internals.

### Sections

> 4.1 [UVs](#s-uvs)

> 4.2 [LODs](#s-lods)

> 4.3 [Modular Socketless Snapping](#s-modular-snapping)

> 4.4 [Must Have Collision](#s-collision)

> 4.5 [Correct Scale](#s-scaled)

<a name="4.1"></a>
<a name="s-uvs"></a>
### 4.1 Static Mesh UVs ![#](https://img.shields.io/badge/lint-supported-green.svg)

If Linter is reporting bad UVs and you can't seem to track it down, open the resulting `.log` file in your project's `Saved/Logs` folder for exact details as to why it's failing. I am hoping to include these messages in the Lint report in the future.

<a name="4.1.1"></a>
<a name="s-uvs-no-missing"></a>
#### 4.1.1 All Meshes Must Have UVs ![#](https://img.shields.io/badge/lint-supported-green.svg)

Pretty simple. All meshes, regardless how they are to be used, should not be missing UVs.

<a name="4.1.2"></a>
<a name="s-uvs-no-overlapping"></a>
#### 4.1.2 All Meshes Must Not Have Overlapping UVs for Lightmaps ![#](https://img.shields.io/badge/lint-supported-green.svg)

Pretty simple. All meshes, regardless how they are to be used, should have valid non-overlapping UVs.

<a name="4.2"></a>
<a name="s-lods"></a>
### 4.2 LODs Should Be Set Up Correctly ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

This is a subjective check on a per-project basis, but as a general rule any mesh that can be seen at varying distances should have proper LODs.

<a name="4.3"></a>
<a name="s-modular-snapping"></a>
### 4.3 Modular Socketless Assets Should Snap To The Grid Cleanly ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

This is a subjective check on a per-asset basis, however any modular socketless assets should snap together cleanly based on the project's grid settings.

It is up to the project whether to snap based on a power of 2 grid or on a base 10 grid. However if you are authoring modular socketless assets for the marketplace, Epic's requirement is that they snap cleanly when the grid is set to 10 units or bigger.

<a name="4.4"></a>
<a name="s-collision"></a>
### 4.4 All Meshes Must Have Collision ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

Regardless of whether an asset is going to be used for collision in a level, all meshes should have proper collision defined. This helps the engine with things such as bounds calculations, occlusion, and lighting. Collision should also be well-formed to the asset.

<a name="4.5"></a>
<a name="s-scaled"></a>
### 4.5 All Meshes Should Be Scaled Correctly ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

This is a subjective check on a per-project basis, however all assets should be scaled correctly to their project. Level designers or blueprint authors should not have to tweak the scale of meshes to get them to confirm in the editor. Scaling meshes in the engine should be treated as a scale override, not a scale correction.

**[⬆ Back to Top](#table-of-contents)**


<a name="5"></a>
<a name="Particle Systems"></a>
<a name="ps"></a>
## 5. Particle Systems ![#](https://img.shields.io/badge/lint-supported-green.svg)

This section will focus on Particle System assets and their internals.

### Sections

> 5.1 [Emitter Naming](#ps-naming)

<a name="5.1"></a>
<a name="ps-emitter-naming"></a>
### 5.1 Emitter Naming ![#](https://img.shields.io/badge/lint-supported-green.svg)

All emitters in a Particle System should be named something descriptive and not left to their default name "Particle Emitter".

**[⬆ Back to Top](#table-of-contents)**


<a name="6"></a>
<a name="Levels"></a>
<a name="levels"></a>
## 6. Levels / Maps ![#](https://img.shields.io/badge/lint-partial_support-yellow.svg)

[See Terminology Note](#terms-level-map) regarding "levels" vs "maps".

This section will focus on Level assets and their internals.

### Sections

> 6.1 [No Errors Or Warnings](#levels-no-errors-or-warnings)

> 6.2 [Lighting Should Be Built](#levels-lighting-should-be-built)

> 6.3 [No Player Visible Z Fighting](#evels-no-visible-z-fighting)

> 6.4 [Marketplace Specific Rules](#evels-levels-mp-rules)

<a name="6.1"></a>
<a name="levels-no-errors-or-warnings"></a>
### 6.1 No Errors Or Warnings ![#](https://img.shields.io/badge/lint-partial_support-yellow.svg)

All levels should load with zero errors or warnings. If a level loads with any errors or warnings, they should be fixed immediately to prevent cascading issues.

You can run a map check on an open level in the editor by using the console command "map check".

Please note: Linter is even more strict on this than the editor is currently, and will catch load errors that the editor will resolve on its own.

<a name="6.2"></a>
<a name="levels-lighting-should-be-built"></a>
### 6.2 Lighting Should Be Built ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

It is normal during development for levels to occasionally not have lighting built. When doing a test/internal/shipping build or any build that is to be distributed however, lighting should always be built.

<a name="6.3"></a>
<a name="levels-no-visible-z-fighting"></a>
### 6.3 No Player Visible Z Fighting ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

Levels should not have any [z-fighting](https://en.wikipedia.org/wiki/Z-fighting) in all areas visible to the player. 

<a name="6.4"></a>
<a name="levels-mp-rules"></a>
### 6.4 Marketplace Specific Rules ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

If a project is to be sold on the UE4 Marketplace, it must follow these rules.

<a name="6.4.1"></a>
<a name="levels-mp-rules-overview"></a>
### 6.4.1 Overview Level ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

If your project contains assets that should be visualized or demoed, you must have a map within your project that contains the name "Overview".

This overview map, if it is visualizing assets, should be set up according to [Epic's guidelines](http://help.epicgames.com/customer/en/portal/articles/2592186-marketplace-submission-guidelines-preparing-your-assets#Required%20Levels%20and%20Maps).

For example, `InteractionComponent_Overview`.

<a name="6.4.2"></a>
<a name="levels-mp-rules-demo"></a>
### 6.4.2 Demo Level ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

If your project contains assets that should be demoed or come with some sort of tutorial, you must have a map within your project that contains the name "Demo". This level should also contain documentation within it in some form that illustrates how to use your project. See Epic's Content Examples project for good examples on how to do this.

If your project is a gameplay mechanic or other form of system as opposed to an art pack, this can be the same as your "Overview" map.

For example, `InteractionComponent_Overview_Demo`, `ExplosionKit_Demo`.

**[⬆ Back to Top](#table-of-contents)**


<a name="7"></a>
<a name="textures"></a>
## 7. Textures ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

This section will focus on Texture assets and their internals.

### Sections

> 7.1 [Dimensions Are Powers of 2](#textures-dimension)

> 7.2 [Texture Density Should Be Uniform](#textures-dimension)

> 7.3 [Textures Should Be No Bigger than 8192](#textures-max-size)

> 7.4 [Correct Texture Groups](#textures-textures-group)

<a name="7.1"></a>
<a name="textures-dimensions"></a>
### 7.1 Dimensions Are Powers of 2 ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

All textures, except for UI textures, must have its dimensions in multiples of powers of 2. Textures do not have to be square.

For example, `128x512`, `1024x1024`, `2048x1024`, `1024x2048`, `1x512`.

<a name="7.2"></a>
<a name="textures-density"></a>
### 7.2 Texture Density Should Be Uniform ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

All textures should be of a size appropriate for their standard use case. Appropriate texture density varies from project to project, but all textures within that project should have a consistent density.

For example, if a project's texture density is 8 pixel per 1 unit, a texture that is meant to be applied to a 100x100 unit cube should be 1024x1024, as that is the closest power of 2 that matches the project's texture density. 

<a name="7.3"></a>
<a name="textures-max-size"></a>
### 7.3 Textures Should Be No Bigger than 8192 ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

No texture should have a dimension that exceeds 8192 in size, unless you have a very explicit reason to do so. Often, using a texture this big is simply just a waste of resources.

<a name="7.4"></a>
<a name="textures-group"></a>
### 7.4 Textures Should Be Grouped Correctly ![#](https://img.shields.io/badge/lint-unsupported-red.svg)

Every texture has a Texture Group property used for LODing, and this should be set correctly based on its use. For example, all UI textures should belong in the UI texture group.

**[⬆ Back to Top](#table-of-contents)**


## Contributors

* [Michael Allar](http://allarsblog.com): [GitHub](https://github.com/Allar), [Twitter](https://twitter.com/michaelallar)
* [CosmoMyzrailGorynych](https://github.com/CosmoMyzrailGorynych)
* [billymcguffin](https://github.com/billymcguffin)
* [akenatsu](https://github.com/akenatsu)

## License

Copyright (c) 2016 Gamemakin LLC

See [LICENSE](/LICENSE)

**[⬆ Back to Top](#table-of-contents)**


## Amendments

We encourage you to fork this guide and change the rules to fit your team's style guide. Below, you may list some amendments to the style guide. This allows you to periodically update your style guide without having to deal with merge conflicts.

# };
