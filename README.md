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

É muito fácil para um membro da equipe usar acidentalmente assets que não estão prontos para uso, o que causará problemas quando esses assets forem removidos. Por exemplo, um artista pode estar iterando em um conjunto modular de static meshs e ainda trabalhando para obter o tamanho e o encaixe da grade corretos. Se um world builders vir esses assets na pasta principal do projeto, ele pode usá-los em um nível sem saber que podem estar sujeitos a mudanças e / ou remoções. Isso causa uma grande quantidade de retrabalho de todos na equipe para resolver.

Se esses ativos modulares fossem colocados em uma pasta de desenvolvedor, o world builders nunca deveria ter um motivo para usá-los e todo o problema nunca aconteceria. O Navegador de conteúdo tem opções de exibição específicas que ocultam as pastas do desenvolvedor (elas ficam ocultas por padrão), tornando impossível o uso acidental de ativos do desenvolvedor em uso normal.

Depois que os recursos estão prontos para uso, o artista simplesmente precisa mover os recursos para a pasta específica do projeto e corrigir os redirecionadores. Isso é essencialmente 'promover' os ativos do experimental para a produção.

<a name="2.4"></a>
<a name="structure-maps"></a>
### 2.4 Todos os arquivos .Map[<sup>*</sup>](#terms-level-map) Pertencem A Uma Pasta Chamada Maps

Os arquivos de mapa são incrivelmente especiais e é comum que cada projeto tenha seu próprio sistema de nomenclatura de mapa, especialmente se trabalhar com sub-levels ou streaming levels. Não importa qual sistema de organização de mapas está em vigor para o projeto específico, todos os níveis devem pertencer a `/Content/Project/Maps`.

Ser capaz de dizer a alguém para abrir um mapa específico sem ter que explicar onde ele está é uma grande economia de tempo e uma melhoria geral da 'qualidade de vida'. É comum os níveis estarem em subpastas de `Maps`, como `Maps/Campaign1/`ou `Maps/Arenas`, mas o mais importante aqui é que todos eles existem em `/Content/Project/Maps`.

Isso também simplifica o trabalho de fazer o cooking para os engenheiros. Combinar os níveis de um processo de compilação pode ser extremamente frustrante se eles tiverem que vasculhar pastas arbitrárias para eles. Se os mapas de uma equipe estão todos em um lugar, é muito mais difícil acidentalmente não criar um mapa em uma construção. Ele também simplifica os scripts de construção de iluminação, bem como os processos de controle de qualidade.

<a name="2.5"></a>
<a name="structure-core"></a>
### 2.5 Use Uma Pasta `Core` Para Blueprints Importantes E Outros Assets

Use a pasta `/Content/Project/Core` para assets que são absolutamente fundamentais para o funcionamento de um projeto. Por exemplo, `GameMode`,` Character`, `PlayerController`,` GameState`, `PlayerState` e Blueprints relacionados devem estar aqui.

Isso cria uma mensagem muito clara "não toque neles" para os outros membros da equipe. Os não engenheiros devem ter muito poucos motivos para entrar na pasta `Core`. Seguindo um bom estilo de estrutura de código, os designers devem fazer seus ajustes de jogabilidade em classes filhas que expõem a funcionalidade. Os World builders deveriam usar Blueprints pré-fabricados em pastas designadas em vez de abusar potencialmente das classes base.

Por exemplo, se seu projeto requer pirckups que podem ser colocados em um level, deve existir uma classe base de pickup em `Core/Pickups` que define o comportamento básico para um Pickup. Pickups específicos como Saúde ou Munição devem existir em uma pasta como `/Content/Project/Placeables/Pickups/`. Os game designers podem definir e ajustar pickups nesta pasta da maneira que quiserem, mas eles não devem tocar em `Core / Pickups`, pois podem quebrar pickups involuntariamente em todo o projeto.

<a name="2.6"></a>
<a name="structure-assettypes"></a>
### 2.6 Não Crie Pastas Chamadas `Assets` ou `AssetTypes`

<a name="2.6.1"></a>
#### 2.6.1 Criar uma pasta chamada `Assets` é redundante.

Todos os assets são assets.

<a name="2.6.2"></a>
#### 2.6.2 Criar uma pasta chamada `Meshes`, `Textures`, ou `Materials` é redundante.

Todos os nomes de assets são nomeados com seu tipo de asset em mente. Essas pastas oferecem apenas informações redundantes e o uso dessas pastas pode ser facilmente substituído pelo sistema de filtragem robusto e fácil de usar que o Content Browser fornece.

Quer ver apenas a malha estática em `Environment/Rocks/`? Basta ativar o filtro Static Mesh. Se todos os assets forem nomeados corretamente, eles também serão classificados em ordem alfabética, independentemente dos prefixos. Deseja visualizar static meshes e skeletal meshes? Basta ligar os dois filtros. Isso elimina a necessidade de selecionar duas pastas com `Control-Click` na visualização em árvore do Content Browser.

> Isso também estende o nome do caminho completo de um asset para muito poucos benefícios. O prefixo `S_` para uma malha estática tem apenas dois caracteres, enquanto` Meshes/ `tem sete caracteres.

Não fazer isso também evita a inevitabilidade de alguém colocar uma malha estática ou uma textura em uma pasta de `Materials`.

<a name="2.7"></a>
<a name="structure-large-sets"></a>
### 2.7 Conjuntos De Assets Muito Grandes Obtêm Seu Próprio Layout De Pasta

Isso pode ser visto como uma pseudo-exceção para [2.6] (# 2.6).

Existem certos tipos de asset que têm um grande volume de arquivos relacionados, onde cada asset  tem uma finalidade única. Os dois mais comuns são asset de animação e áudio. Se você tiver mais de 15 desses asset que pertencem um ao outro, eles deveriam estar juntos.

Por exemplo, as animações que são compartilhadas por vários personagens devem ser colocadas em `Characters/Common/Animations` e podem ter subpastas como` Locomotion` ou `Cinematic`.

> Isso não se aplica a assets como texturas e materiais. É comum que uma pasta `Rocks` tenha uma grande quantidade de texturas se houver uma grande quantidade de pedras, no entanto, essas texturas geralmente estão relacionadas apenas a algumas pedras específicas e devem ser nomeadas apropriadamente. Mesmo que essas texturas façam parte de uma [MaterialLibrary] (# 2.8).

<a name="2.8"></a>
<a name="structure-material-library"></a>
### 2.8 `MaterialLibrary`

Se o seu projeto faz uso de master materials, layered materials ou qualquer forma de materiais ou texturas reutilizáveis que não pertencem a nenhum subconjunto de assets, esses assets devem estar localizados em `Content/Project/MaterialLibrary`.

Desta forma, todos os materiais 'globais' têm um lugar para morar e são facilmente localizados.

> Isso também torna incrivelmente fácil aplicar uma política de 'usar apenas instâncias de materiais' em um projeto. Se todos os artistas e assets deveriam estar usando material instances, então os únicos Assets de materiais regulares que deveriam existir estão dentro desta pasta. Você pode verificar isso facilmente procurando por materiais básicos em qualquer pasta que não seja a `MaterialLibrary`.

O `MaterialLibrary` não precisa consistir apenas em materiais. Texturas de utilitários compartilhadas, material functions e outras coisas dessa natureza devem ser armazenadas aqui também em pastas que indicam a finalidade pretendida. Por exemplo, texturas de noise genéricas devem estar localizadas em `MaterialLibrary/Utility`.

Qualquer material de teste ou depuração deve estar dentro de `MaterialLibrary/Debug`. Isso permite que os materiais de depuração sejam facilmente retirados de um projeto antes do envio e torna incrivelmente aparente se os ativos de produção os estão usando se forem mostrados erros de referência.

<a name="2.9"></a>
<a name="structure-no-empty-folders"></a>
### 2.9 Sem Pastas Vazias

Simplesmente não deve haver pastas vazias. Eles confundem o content browser.

Se você achar que o content browser tem uma pasta vazia que não pode ser excluída, faça o seguinte:
1. Certifique-se de usar o Source Control.
1. Execute imediatamente Fix Up Redirectors em seu projeto.
1. Navegue até a pasta no disco e exclua os ativos dentro dela.
1. Feche o editor.
1. Certifique-se de que seu estado do Source Control está sincronizado (ou seja, se estiver usando Perforce, execute um Reconcile Offline Work em seu diretório de conteúdo)
1. Abra o editor. Confirme se tudo ainda funciona conforme o esperado. Caso contrário, reverta, descubra o que deu errado e tente novamente.
1. Certifique-se de que a pasta tenha desaparecido.
1. Envie as alterações para o Source Control.

**[⬆ Voltar ao Topo](#table-of-contents)**


<a name="3"></a>
<a name="bp"></a>
## 3. Blueprints

Esta seção se concentrará nas classes Blueprint e seus componentes internos. Quando possível, as regras de estilo estão em conformidade com o [Epic's Coding Standard] (https://docs.unrealengine.com/latest/INT/Programming/Development/CodingStandard).

Lembre-se: o projeto não suporta erros graves, cuidado! (Frase de [KorkuVeren] (http://github.com/KorkuVeren))

### Seções

> 3.1 [Compiling](#bp-compiling)

> 3.2 [Variables](#bp-vars)

> 3.3 [Functions](#bp-functions)

> 3.4 [Graphs](#bp-graphs)

<a name="3.1"></a>
<a name="bp-compiling"></a>
### 3.1 Compiling

Todos os blueprints devem ser compilados com nenhum aviso e nenhum erro. Você deve corrigir os avisos e erros do blueprint imediatamente, pois eles podem rapidamente se transformar em um comportamento inesperado muito assustador.

* Não * envie projetos corrompidos ao controle de origem. Se você precisar armazená-los no controle de origem, arquive-os.

Projetos corrompidos podem causar problemas que se manifestam de outras maneiras, como referências quebradas, comportamento inesperado, falhas de cooking e recompilação desnecessária frequente. Um projeto quebrado tem o poder de quebrar todo o seu jogo.

<a name="3.2"></a>
<a name="bp-vars"></a>
### 3.2 Variables

As palavras `variable` e` property` podem ser usadas indistintamente.

#### Seções

> 3.2.1 [Naming](#bp-vars)

> 3.2.2 [Editable](#bp-vars-editable)

> 3.2.3 [Categories](#bp-vars-categories)

> 3.2.4 [Access](#bp-vars-access)

> 3.2.5 [Advanced](#bp-vars-advanced)

> 3.2.6 [Transient](#bp-vars-transient)

> 3.2.7 [Config](#bp-vars-config)

<a name="3.2.1"></a>
<a name="bp-var-naming"></a>
#### 3.2.1 Naming

<a name="3.2.1.1"></a>
<a name="bp-var-naming-nouns"></a>
##### 3.2.1.1 Substantivos

Todos os nomes de variáveis não booleanas devem ser substantivos claros, não ambíguos e descritivos.

<a name="3.2.1.2"></a>
<a name="bp-var-naming-case"></a>
##### 3.2.1.2 PascalCase

Todas as variáveis não booleanas devem estar na forma de[PascalCase](#terms-cases).

<a name="3.2.1.2.1"></a>
###### 3.2.1.2.1 Exemplos:

* `Score`
* `Kills`
* `TargetPlayer`
* `Range`
* `CrosshairColor`
* `AbilityID`

<a name="3.2.1.3"></a>
<a name="bp-var-bool-prefix"></a>
##### 3.2.1.3 Boolean `b` Prefix

Todos as booleanas devem ser nomeadas em PascalCase, mas prefixadas com `b` minúsculo.

Exemplo: Use `bDead` e` bEvil`, ** não ** `Dead` e` Evil`.

Os editores do UE4 Blueprint não devem incluir o `b` em exibições user-friendly da variável.

<a name="3.2.1.4"></a>
<a name="bp-var-bool-names"></a>
##### 3.2.1.4 Boolean Names

<a name="3.2.1.4.1"></a>
###### 3.2.1.4.1 Informações Gerais e de Estados Independentes

Todos as booleanas devem ser nomeadas como adjetivos descritivos, quando possível, se representarem informações gerais. Não inclua palavras que expressem a variável como uma pergunta, como `Is`. Isso é reservado para funções.

Exemplo: Use `bDead` e` bHostile` ** e não ** `bIsDead` e` bIsHostile`.

Tente não usar verbos como `bRunning`. Os verbos tendem a levar a estados complexos.

<a name="3.2.1.4.2"></a>
###### 3.2.1.4.2 Estados Complexos

Não use booleanas para representar estados complexos e / ou dependentes. Isso torna a adição e remoção de estados complexa e não mais facilmente legível. Em vez disso, use uma enumeração.

Exemplo: Ao definir uma arma, ** não ** use `bReloading` e` bEquipping` se uma arma não puder recarregar e equipar. Defina uma enumeração chamada `EWeaponState` e use uma variável com este tipo chamada` WeaponState`. Isso torna muito mais fácil adicionar novos estados às armas.

Exemplo: ** não ** use `bRunning` se também precisar de` bWalking` ou `bSprinting`. Isso deve ser definido como uma enumeração com nomes de estado claramente definidos.

<a name="3.2.1.5"></a>
<a name="bp-vars-naming-context"></a>
##### 3.2.1.5 Considere o Contexto

Todos os nomes de variáveis não devem ser redundantes com seu contexto, pois todas as referências de variáveis no Blueprint sempre terão contexto.

<a name="3.2.1.5e"></a>
###### 3.2.1.5e Exemplos:

Considere um Blueprint chamado `BP_PlayerCharacter`.

**Bad**

* `PlayerScore`
* `PlayerKills`
* `MyTargetPlayer`
* `MyCharacterName`
* `CharacterSkills`
* `ChosenCharacterSkin`

Todas essas variáveis são nomeadas de forma redundante. Está implícito que a variável é representativa do `BP_PlayerCharacter` ao qual pertence, porque é` BP_PlayerCharacter` que está definindo essas variáveis.

**Good**

* `Score`
* `Kills`
* `TargetPlayer`
* `Name`
* `Skills`
* `Skin`

<a name="3.2.1.6"></a>
<a name="bp-vars-naming-atomic"></a>
##### 3.2.1.6 _Não_ Inclua Nomes de Tipos Atômicos

Variáveis atômicas ou primitivas são variáveis que representam dados em sua forma mais simples, como booleanos, inteiros, flutuantes e enumerações.

Strings e vetores são considerados atômicos em termos de estilo ao trabalhar com Blueprints, no entanto, eles não são tecnicamente atômicos.

> Embora os vetores consistam em três floats, os vetores geralmente podem ser manipulados como um todo, o mesmo com os rotators.

> _Não_ considere as variáveis de texto como atômicas, elas ocultam secretamente a funcionalidade de localização. O tipo atômico de uma string de caracteres é `String`, não` Text`.

Variáveis atômicas não devem ter seu nome de tipo em seu nome.

Exemplo: Use `Score`,` Kills` e `Description` ** e não **` ScoreFloat`, `FloatKills`,` DescriptionString`.

A única exceção a esta regra é quando uma variável representa 'um número de' algo a ser contado _e_ quando usar um nome sem um tipo de variável não é fácil de ler.

Exemplo: Um Fence Generator precisa gerar um número X de posts. Armazene o X em `NumPosts` ou` PostsCount` em vez de `Posts`, pois` Posts` podem potencialmente ser lidos como um Array de um tipo de variável chamado `Post`.

<a name="3.2.1.7"></a>
<a name="bp-vars-naming-complex"></a>
##### 3.2.1.7 Inclua Nomes De Tipo Não Atômico

Variáveis não atômicas ou complexas são variáveis que representam dados como uma coleção de variáveis atômicas. Structs, Classes, Interfaces e primitivos com comportamento oculto, como `Texto` e` Nome`, todos se qualificam sob esta regra.

> Embora um Array de um tipo de variável atômica seja uma lista de variáveis, os Arrays não mudam a 'atomicidade' de um tipo de variável.

Essas variáveis devem incluir seu nome de tipo, ainda considerando seu contexto.

Se uma classe possui uma instância de uma variável complexa, ou seja, se um `BP_PlayerCharacter` possui um` BP_Hat`, ele deve ser armazenado como o tipo de variável, sem qualquer modificação de nome.

Exemplo: Use `Hat`,` Flag` e `Ability` ** e não **` MyHat`, `MyFlag` e` PlayerAbility`.

Se uma classe não possui o valor que uma variável complexa representa, você deve usar um substantivo junto com o tipo de variável.

Exemplo: Se um `BP_Turret` tem a capacidade de direcionar um` BP_PlayerCharacter`, ele deve armazenar seu destino como `TargetPlayer` como quando no contexto de` BP_Turret` deve ficar claro que é uma referência a outro tipo de variável complexa que ele não possui.


<a name="3.2.1.8"></a>
<a name="bp-vars-naming-arrays"></a>
##### 3.2.1.8 Arrays

Os arrays seguem as mesmas regras de nomenclatura acima, mas devem ser nomeados como um substantivo no plural.

Exemplo: use `Targets`,` Hats` e `EnemyPlayers`, ** não **` TargetList`, `HatArray`,` EnemyPlayerArray`.


<a name="3.2.2"></a>
<a name="bp-vars-editable"></a>
#### 3.2.2 Variáveis Editáveis

Todas as variáveis que podem ser alteradas com segurança para configurar o comportamento de um blueprint devem ser marcadas como `Editáveis`.

Por outro lado, todas as variáveis que não são seguras para alterar ou não devem ser expostas aos designers _não_ devem ser marcadas como editáveis, a menos que por razões de engenharia a variável deva ser marcada como `Expose On Spawn`.

Não marque variáveis arbitrariamente como `Editable`.

<a name="3.2.2.1"></a>
<a name="bp-vars-editable-tooltips"></a>
##### 3.2.2.1 Tooltips

Todas as variáveis `Editable`, incluindo aquelas marcadas como editáveis apenas para que possam ser marcadas como` Expose On Spawn`, devem ter uma descrição em seus campos `Tooltip` que explica como alterar este valor afeta o comportamento do blueprint.

<a name="3.2.2.2"></a>
<a name="bp-vars-editable-ranges"></a>
##### 3.2.2.2 Slider e Value Ranges

Todas as variáveis `editáveis` devem fazer uso do slider e value ranges se houver um valor para o qual uma variável _não_ deve ser definida.

Exemplo: Um blueprint que gera postes de cerca pode ter uma variável editável chamada `PostsCount` e um valor -1 não faria nenhum sentido. Use os campos de intervalo para marcar 0 como o mínimo.

Se uma variável editável for usada em um Script de Construção, ela deve ter um Slider Range razoável definido para que alguém não possa acidentalmente atribuir a ela um valor grande que pode travar o editor.

Um Value Range só precisa ser definido se os limites de um valor forem conhecidos. Enquanto um Slider Range evita entradas acidentais de grandes números, um Value Range indefinido permite que um usuário especifique um valor fora do Slider Range que pode ser considerado 'perigoso', mas ainda válido.

<a name="3.2.3"></a>
<a name="bp-vars-categories"></a>
#### 3.2.3 Categories

Se uma classe tiver apenas um pequeno número de variáveis, as categorias não são necessárias.

Se uma classe tem uma quantidade moderada de variáveis (5-10), todas as variáveis `Editable` devem ter uma categoria não padrão atribuída. Uma categoria comum é `Config`.

Se uma classe tem uma grande quantidade de variáveis, todas as variáveis `Editable` devem ser categorizadas em subcategorias usando a categoria` Config` como a categoria base. Variáveis não editáveis devem ser categorizadas em categorias descritivas que descrevem seu uso.

> Você pode definir subcategorias usando a barra vertical `|`, ou seja, `Config | Animations`.

Exemplo: um conjunto de variáveis de classe de arma pode ser organizado como:

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
#### 3.2.4 Variable Access Level

Em C ++, as variáveis têm um conceito de nível de acesso. Public significa que qualquer código fora da classe pode acessar a variável. Protected significa que apenas a classe e quaisquer classes filhas podem acessar essa variável internamente. Private significa que apenas esta classe e nenhuma classe filha pode acessar esta variável.

Os blueprints não têm um conceito definido de acesso Protected atualmente.

Trate as variáveis `Editable` como variáveis public. Trate as variáveis não editáveis como variáveis protegidas.

<a name="3.2.4.1"></a>
<a name="bp-vars-access-private"></a>
##### 3.2.4.1 Private Variables

A menos que se saiba que uma variável só deve ser acessada dentro da classe em que está definida e nunca em uma classe filha, não marque as variáveis como private. Até que as variáveis possam ser marcadas como `protected`, reserve privado para quando você tiver certeza absoluta de que deseja restringir o uso da classe filha.

<a name="3.2.5"></a>
<a name="bp-vars-advanced"></a>
#### 3.2.5 Advanced Display

Se uma variável deve ser editável, mas frequentemente intocada, marque-a como `Advanced Display`. Isso torna a variável oculta, a menos que a seta de exibição avançada seja clicada.

Para encontrar a opção `Advanced Display`, ela é listada como uma advanced displayed variable na lista de detalhes da variável.

<a name="3.2.6"></a>
<a name="bp-vars-transient"></a>
#### 3.2.6 Transient Variables

Variáveis transitórias são variáveis que não precisam ter seu valor salvo e carregado e possuem um valor inicial igual a zero ou nulo. Isso é útil para referências a outros objetos e atores cujo valor não é conhecido até o tempo de execução. Isso evita que o editor salve uma referência a ele e acelera o salvamento e o carregamento da classe de blueprint.

Por causa disso, todas as variáveis transientes sempre devem ser inicializadas como zero ou nulas. Fazer o contrário resultaria em erros difíceis de depurar.

<a name="3.2.7"></a>
<a name="bp-vars-config"></a>
#### 3.2.8 Config Variables

Não use o sinalizador `Config Variable`. Isso torna mais difícil para os designers controlar o comportamento do blueprint. Variáveis de configuração só devem ser usadas em C ++ para variáveis raramente alteradas. Pense neles como variáveis de `Advanced Advanced Display`.

<a name="3.3"></a>
<a name="bp-functions"></a>
### 3.3 Functions, Events, e Event Dispatchers

Esta seção descreve como você deve criar functions, events e event dispatchers. Tudo o que se aplica a funções também se aplica a eventos, a menos que indicado de outra forma.

<a name="3.3.1"></a>
<a name="bp-funcs-naming"></a>
#### 3.3.1 Function Naming

A nomenclatura de functions, events e event dispatchers é extremamente importante. Com base apenas no nome, certas suposições podem ser feitas sobre as funções. Por exemplo:

* É uma função pura?
* Ele está buscando informações de estado?
* É um manipulador?
* É um RPC?
* Qual é seu propósito?

Essas perguntas e muito mais podem ser respondidas quando as funções são nomeadas apropriadamente.

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
