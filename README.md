<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>🌿 Sertão Vivo · Espécies da Caatinga & Agrícolas</title>
  
  <script src="https://cdn.tailwindcss.com"></script>
  
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400..900;1,400..900&family=Plus+Jakarta+Sans:ital,wght@0,200..800;1,200..800&display=swap" rel="stylesheet">

  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            sans: ['"Plus Jakarta Sans"', 'sans-serif'],
            serif: ['"Playfair Display"', 'serif'],
          },
          colors: {
            sertao: {
              50: '#fbfaf7',
              100: '#f4f0e6',
              200: '#e7decb',
              300: '#d5c7a9',
              400: '#beaa81',
              500: '#aa9261',
              600: '#91774b',
              700: '#79603e',
              800: '#634e35',
              900: '#4d3d2a',
            },
            caatinga: {
              50: '#f3f7f3',
              100: '#e4eee3',
              200: '#cbdcc9',
              300: '#a4c2a1',
              400: '#75a071',
              500: '#53824f',
              600: '#40683c',
              700: '#345331',
              800: '#2b4429',
              900: '#213520',
            },
            agricola: {
              50: '#fdfbeb',
              100: '#fcf6cd',
              500: '#d9a71e',
              600: '#b88414',
              700: '#946210',
            }
          }
        }
      }
    }
  </script>

  <style>
    body {
      background-color: #f6f3eb;
      background-image: 
        radial-gradient(at 0% 0%, rgba(228, 238, 227, 0.4) 0px, transparent 50%),
        radial-gradient(at 100% 100%, rgba(213, 199, 169, 0.3) 0px, transparent 50%);
    }
    .card {
      transition: all 0.3s ease;
    }
    .card:hover {
      transform: translateY(-4px);
    }
    .emoji-big {
      font-size: 4.5rem;
      line-height: 1;
      display: block;
      text-align: center;
      padding: 1.5rem 0;
      filter: drop-shadow(0 4px 8px rgba(0,0,0,0.1));
    }
    .curiosidade-card {
      background: linear-gradient(135deg, #f8f5ee, #f0ece3);
      border-left: 4px solid #53824f;
      padding: 1rem;
      border-radius: 1rem;
      margin-top: 0.5rem;
    }
    .curiosidade-card .label {
      font-size: 0.65rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.05em;
      color: #53824f;
    }
    .modal-emoji-big {
      font-size: 5rem;
      line-height: 1;
      text-align: center;
      padding: 1rem;
    }
    .info-tag {
      display: inline-block;
      padding: 0.25rem 0.75rem;
      border-radius: 9999px;
      font-size: 0.6rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.05em;
    }
    .info-tag.medicinal { background: #d4edda; color: #155724; }
    .info-tag.alimenticio { background: #fff3cd; color: #856404; }
    .info-tag.industrial { background: #cce5ff; color: #004085; }
    .info-tag.sagrado { background: #e8daef; color: #6c3483; }
    .info-tag.perigo { background: #f8d7da; color: #721c24; }
    .info-tag.artesanato { background: #fce4ec; color: #880e4f; }
  </style>
</head>
<body class="min-h-screen font-sans text-stone-800 antialiased selection:bg-caatinga-200 selection:text-caatinga-900">

  <header class="relative overflow-hidden py-16 sm:py-24 border-b border-sertao-200/60 bg-gradient-to-b from-caatinga-50/50 to-transparent">
    <div class="max-w-6xl mx-auto px-6 text-center relative z-10">
      <span class="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs font-semibold tracking-wider text-caatinga-700 bg-caatinga-100/80 border border-caatinga-200 mb-6 uppercase">
        🌱 Biodiversidade & Cultivo
      </span>
      <h1 class="font-serif text-4xl sm:text-6xl font-bold text-caatinga-900 tracking-tight mb-4">
        Raízes do Sertão
      </h1>
      <p class="text-stone-600 max-w-xl mx-auto text-sm sm:text-base font-medium leading-relaxed">
        Descubra os segredos, usos e curiosidades de cada espécie. Clique nos cards e surpreenda-se!
      </p>
    </div>
  </header>

  <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
    <div class="bg-white/70 backdrop-blur-md rounded-3xl p-6 mb-12 shadow-sm border border-white/80 flex flex-col lg:flex-row gap-4 items-center justify-between">
      
      <div class="relative w-full lg:w-80">
        <span class="absolute inset-y-0 left-0 flex items-center pl-4 pointer-events-none text-stone-400">
          🔍
        </span>
        <input 
          type="text" 
          id="searchInput" 
          placeholder="Buscar espécie, solo ou ameaça..." 
          class="w-full pl-11 pr-4 py-3 bg-stone-100/80 border border-stone-200/80 rounded-2xl text-sm focus:outline-none focus:ring-2 focus:ring-caatinga-400/50 focus:border-caatinga-500 transition-all placeholder:text-stone-400"
        >
      </div>

      <div class="flex flex-wrap gap-2 w-full lg:w-auto justify-start lg:justify-end">
        <button onclick="filtrarEspesies('todas')" id="btn-todas" class="btn-filtro px-4 py-2.5 rounded-xl text-xs font-semibold transition-all bg-caatinga-800 text-white shadow-sm">
          Ver Todas (<span id="count-todas">32</span>)
        </button>
        <button onclick="filtrarEspesies('agricola')" id="btn-agricola" class="btn-filtro px-4 py-2.5 rounded-xl text-xs font-semibold transition-all bg-stone-100 text-stone-600 hover:bg-stone-200/70 border border-stone-200/50">
          🌾 Culturas Agrícolas
        </button>
        <button onclick="filtrarEspesies('seguras')" id="btn-seguras" class="btn-filtro px-4 py-2.5 rounded-xl text-xs font-semibold transition-all bg-stone-100 text-stone-600 hover:bg-stone-200/70 border border-stone-200/50">
          Comestíveis/Nativas
        </button>
        <button onclick="filtrarEspesies('toxicas')" id="btn-toxicas" class="btn-filtro px-4 py-2.5 rounded-xl text-xs font-semibold transition-all bg-stone-100 text-stone-600 hover:bg-stone-200/70 border border-stone-200/50">
          Alertas/Tóxicas
        </button>
        <button onclick="filtrarEspesies('ameacadas')" id="btn-ameacadas" class="btn-filtro px-4 py-2.5 rounded-xl text-xs font-semibold transition-all bg-stone-100 text-stone-600 hover:bg-stone-200/70 border border-stone-200/50">
          Sob Ameaça
        </button>
      </div>
    </div>

    <div class="mb-6 flex justify-between items-center px-2">
      <h2 class="text-xs font-bold uppercase tracking-widest text-stone-400">
        Catálogo Geral
      </h2>
      <p class="text-xs font-semibold text-caatinga-700 bg-caatinga-100/50 px-2.5 py-1 rounded-full border border-caatinga-200/40">
        Mostrando <span id="contadorExibido">32</span> de 32
      </p>
    </div>

    <div id="plantaGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
    </div>

    <div id="emptyState" class="hidden text-center py-24 bg-white/40 rounded-3xl border border-dashed border-stone-300">
      <span class="text-4xl block mb-3">🌾</span>
      <h3 class="text-lg font-bold text-stone-700">Nenhuma espécie agrícola ou nativa encontrada</h3>
      <p class="text-sm text-stone-500">Tente buscar por termos diferentes ou altere o filtro de seleção.</p>
    </div>
  </main>

  <!-- MODAL COM INFORMAÇÕES ÚNICAS -->
  <div id="plantaModal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-stone-900/60 backdrop-blur-sm hidden transition-opacity duration-300 opacity-0">
    <div class="bg-white w-full max-w-2xl rounded-[2.5rem] overflow-hidden shadow-2xl border border-stone-200/80 transform scale-95 transition-transform duration-300 max-h-[90vh] overflow-y-auto">
      
      <div class="p-6 md:p-8">
        <div class="flex justify-between items-start mb-2">
          <div class="flex items-center gap-4">
            <span id="modalEmoji" class="text-5xl"></span>
            <h3 id="modalNome" class="font-serif text-2xl md:text-3xl font-bold text-stone-900 tracking-tight"></h3>
          </div>
          <button onclick="fecharModal()" class="text-stone-400 hover:text-stone-700 text-3xl p-1 font-semibold leading-none">&times;</button>
        </div>
        
        <div class="flex flex-wrap gap-2 mt-2 mb-4" id="modalTags"></div>
        
        <p id="modalDesc" class="text-sm text-stone-600 italic leading-relaxed mb-4 border-l-4 border-caatinga-400 pl-4"></p>

        <!-- INFORMAÇÕES ÚNICAS - O DIFERENCIAL DO SITE -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-4">
          <div class="curiosidade-card">
            <div class="label">📜 Curiosidade</div>
            <p id="modalCuriosidade" class="text-sm text-stone-700 mt-1 leading-relaxed"></p>
          </div>
          <div class="curiosidade-card" style="border-left-color: #d4856a;">
            <div class="label">💡 Uso Tradicional</div>
            <p id="modalUso" class="text-sm text-stone-700 mt-1 leading-relaxed"></p>
          </div>
          <div class="curiosidade-card" style="border-left-color: #f5d742;">
            <div class="label">🌟 Benefício</div>
            <p id="modalBeneficio" class="text-sm text-stone-700 mt-1 leading-relaxed"></p>
          </div>
          <div class="curiosidade-card" style="border-left-color: #8B7D6B;">
            <div class="label">🌍 Significado Cultural</div>
            <p id="modalCultural" class="text-sm text-stone-700 mt-1 leading-relaxed"></p>
          </div>
        </div>

        <div class="mt-6 pt-4 border-t border-stone-100 grid grid-cols-2 gap-3">
          <div class="text-xs bg-stone-50 p-3 rounded-xl">
            <span class="block font-extrabold uppercase text-[10px] tracking-wider text-caatinga-700">🌱 Solo</span>
            <p id="modalSolo" class="text-stone-600 font-medium"></p>
          </div>
          <div class="text-xs bg-stone-50 p-3 rounded-xl">
            <span class="block font-extrabold uppercase text-[10px] tracking-wider text-red-700">⚠️ Alertas</span>
            <p id="modalVeneno" class="text-stone-600 font-medium"></p>
          </div>
        </div>

        <div class="mt-4 pt-4 border-t border-stone-100 flex justify-between items-center">
          <span id="modalAmeacas" class="text-xs text-amber-700 font-medium"></span>
          <button onclick="fecharModal()" class="px-5 py-2.5 rounded-xl bg-stone-900 text-white text-xs font-semibold hover:bg-stone-800 transition-colors shadow-sm">
            Fechar
          </button>
        </div>
      </div>

    </div>
  </div>

  <footer class="border-t border-sertao-200 bg-stone-100/50 py-12 mt-20 text-center">
    <div class="max-w-7xl mx-auto px-6 flex flex-col items-center gap-4">
      <span class="inline-flex items-center gap-1.5 px-4 py-1.5 rounded-full text-xs font-bold text-caatinga-800 bg-sertao-200/60 border border-sertao-300/40">
        🌱 Sertão Vivo · Conhecer para Conservar
      </span>
      <p class="text-xs text-stone-500">
        Plataforma informativa focada na preservação e no desenvolvimento sustentável do semiárido.
      </p>
    </div>
  </footer>

  <script>
    (function() {
      const especies = [
        // --- CULTURAS AGRÍCOLAS ---
        {
          nome: "Algodoeiro",
          desc: "Planta cultivada para produção de fibras têxteis, adaptada ao semiárido nordestino.",
          solo: "Arenosos e profundos, bem adaptado a solos de baixa fertilidade.",
          veneno: "Não tóxico para humanos. Caroço cru tem gossipol.",
          ameacas: "Praga do bicudo-do-algodoeiro e desestímulo do mercado tradicional.",
          tags: ["agricola"],
          emoji: "🌾",
          curiosidade: "O algodão é cultivado há mais de 7.000 anos! As civilizações antigas já usavam suas fibras para fazer tecidos.",
          uso: "Fibras para tecidos, óleo das sementes, ração animal e produção de papel-moeda.",
          beneficio: "O óleo de algodão é rico em vitamina E e é usado na culinária e cosméticos.",
          cultural: "O algodão foi um dos principais motores da revolução industrial e da economia nordestina."
        },
        {
          nome: "Milho",
          desc: "Cereal de ciclo super precoce selecionado para produzir grãos mesmo em períodos curtos de chuva.",
          solo: "Férteis, bem drenados, arenosos ou franco-argilosos.",
          veneno: "Totalmente seguro e comestível.",
          ameacas: "Estios prolongados no período de floração e ataque da lagarta-do-cartucho.",
          tags: ["agricola", "segura"],
          emoji: "🌽",
          curiosidade: "O milho é uma planta que não existe na natureza! Foi completamente domesticado pelos povos indígenas há mais de 10.000 anos.",
          uso: "Alimentação humana e animal, produção de farinhas, óleos, biocombustíveis e plásticos biodegradáveis.",
          beneficio: "Rico em carboidratos, fibras, vitaminas do complexo B e antioxidantes como a zeaxantina.",
          cultural: "Sagrado para diversas culturas indígenas, o milho é celebrado em festas e rituais em todo o continente americano."
        },
        {
          nome: "Soja",
          desc: "Cultivares de soja desenvolvidas e adaptadas para transições de cerrado/caatinga.",
          solo: "Planos, profundos, bem corrigidos (exige calagem e adubação fosfatada).",
          veneno: "Seguro após processamento. Grão cru possui fatores antinutricionais.",
          ameacas: "Veranicos intensos e degradação física de solos frágeis por monocultura.",
          tags: ["agricola"],
          emoji: "🫘",
          curiosidade: "A soja é conhecida como a 'carne vegetal' e contém todos os aminoácidos essenciais para a nutrição humana.",
          uso: "Produção de óleo, leite de soja, tofu, farinha, ração animal e biocombustíveis.",
          beneficio: "Rica em proteínas, isoflavonas (antioxidantes), ferro e cálcio. Ajuda a reduzir o colesterol.",
          cultural: "Originária da Ásia, a soja é um dos alimentos mais antigos cultivados pelo homem, há mais de 5.000 anos."
        },
        {
          nome: "Trigo",
          desc: "Variedade experimental adaptada ao calor, cultivada em regime de irrigação ou plantio direto.",
          solo: "Férteis, profundos e argilo-arenosos com boa retenção hídrica.",
          veneno: "Não tóxico. Fonte de alimento básica universal.",
          ameacas: "Doença da brusone do trigo e dependência crítica de manejo de irrigação.",
          tags: ["agricola"],
          emoji: "🌾",
          curiosidade: "O trigo foi um dos primeiros cereais a ser cultivado, há cerca de 10.000 anos, no Crescente Fértil.",
          uso: "Farinhas para pães, massas, bolos, cerveja, ração animal e biocombustíveis.",
          beneficio: "Fonte de carboidratos complexos, fibras, proteínas, vitaminas do complexo B e minerais.",
          cultural: "O trigo é símbolo de prosperidade e abundância em muitas culturas, presente em mitos e celebrações."
        },
        {
          nome: "Feijão-Caupi",
          desc: "Conhecido como feijão-de-corda, é a principal leguminosa alimentar e de cobertura do Nordeste.",
          solo: "Leves, arenosos ou franco-arenosos de rápida drenagem.",
          veneno: "Totalmente seguro e altamente proteico.",
          ameacas: "Períodos de seca severa antes da maturação das vagens.",
          tags: ["agricola", "segura"],
          emoji: "🫘",
          curiosidade: "O feijão-caupi é tão resistente à seca que consegue produzir mesmo em anos de estiagem severa!",
          uso: "Alimentação humana (cozido), ração animal, adubação verde e fixação de nitrogênio no solo.",
          beneficio: "Excelente fonte de proteína vegetal, fibras, ferro, potássio e vitaminas do complexo B.",
          cultural: "É o prato principal do famoso 'baião de dois' nordestino, símbolo da culinária do sertão."
        },
        {
          nome: "Sorgo",
          desc: "Substituto direto do milho para nutrição animal; consome consideravelmente menos água.",
          solo: "Tolerante a solos marginais, salinos e moderadamente ácidos.",
          veneno: "Plantas muito jovens/brotos podem conter ácido cianídrico.",
          ameacas: "Ataque severo de pulgões e pássaros na fase de grãos leitosos.",
          tags: ["agricola", "toxica"],
          emoji: "🌾",
          curiosidade: "O sorgo é uma das plantas mais eficientes em usar água, precisando de 1/3 da água que o milho necessita!",
          uso: "Alimentação animal, produção de farinha (para celíacos), etanol e vassouras.",
          beneficio: "Rico em antioxidantes, fibras e ferro. Não contém glúten, sendo ótimo para celíacos.",
          cultural: "Originário da África, o sorgo é cultivado há mais de 5.000 anos e é um alimento básico em muitos países."
        },
        {
          nome: "Gergelim",
          desc: "Oleaginosa rústica e de alto valor de mercado adaptada ao calor extremo do Nordeste.",
          solo: "Arenosos, leves, profundos e sem risco de encharcamento.",
          veneno: "Totalmente seguro, saudável e rico em óleos essenciais.",
          ameacas: "Ausência de colheita mecanizada de pequeno porte adaptada à região.",
          tags: ["agricola", "segura"],
          emoji: "🌱",
          curiosidade: "O gergelim é uma das oleaginosas mais antigas do mundo, com registros de cultivo há mais de 4.000 anos na Índia!",
          uso: "Óleo culinário, confeitaria (pães, doces), tahine (pasta), cosméticos e medicamentos.",
          beneficio: "Rico em cálcio, ferro, magnésio, fósforo, vitamina E e gorduras saudáveis. Fortalece ossos e dentes.",
          cultural: "Na cultura árabe, o gergelim é tão valorizado que a expressão 'abre-te, sésamo' imortalizou a planta na literatura."
        },
        {
          nome: "Mamona",
          desc: "Cultivada para produção de óleo industrial de altíssima resistência térmica.",
          solo: "Profundos, arenosos ou argilosos bem drenados e de fertilidade média.",
          veneno: "Altamente tóxico! Suas sementes contêm ricina, uma das toxinas naturais mais potentes.",
          ameacas: "Oscilações drásticas nos preços de mercado e praga do mofo-cinzento.",
          tags: ["agricola", "toxica"],
          emoji: "⚠️",
          curiosidade: "A ricina da mamona é uma toxina tão poderosa que uma única semente pode matar uma criança. Mas o óleo, quando processado, é totalmente seguro!",
          uso: "Óleo industrial (lubrificantes, tintas, plásticos), biocombustíveis e medicamentos (como laxante).",
          beneficio: "O óleo de mamona é usado na indústria aeroespacial como lubrificante de alta performance!",
          cultural: "A mamona era cultivada pelos antigos egípcios para iluminação de templos e tratamento de doenças."
        },

        // --- ESPÉCIES NATIVAS ---
        { 
          nome: "Umbuzeiro", 
          desc: "Fruto doce e suculento. Árvore sagrada do semiárido que armazena água em suas raízes.",
          solo: "Arenosos, profundos, bem drenados e de baixa fertilidade.",
          veneno: "Totalmente seguro. Seus frutos e folhas são altamente comestíveis.",
          ameacas: "Desmatamento e sobrepastoreio, que impedem o nascimento de novas mudas.",
          tags: ["segura"],
          emoji: "🍐",
          curiosidade: "O umbuzeiro é conhecido como a 'árvore sagrada do sertão' porque suas raízes armazenam até 1.000 litros de água!",
          uso: "Frutos consumidos in natura, sucos, doces, sorvetes e geleias. Sombra para animais.",
          beneficio: "Rico em vitaminas A e C, cálcio e ferro. Hidrata e nutre no período da seca.",
          cultural: "O umbu é tão importante que deu nome à cidade de Umbuzeiro na Paraíba. Faz parte da identidade sertaneja."
        },
        { 
          nome: "Carnaúba", 
          desc: "Palmeira que fornece cera, palha e frutos. Conhecida como a 'árvore da vida'.",
          solo: "Argilosos e úmidos, típicos de várzeas e margens de rios.",
          veneno: "Não tóxica. Praticamente todas as partes da planta são aproveitadas.",
          ameacas: "Invasão da planta exótica unha-de-gato e corte desordenado.",
          tags: ["segura"],
          emoji: "🌴",
          curiosidade: "A cera da carnaúba é tão resistente que é usada em móveis de luxo, na indústria automotiva e até em alimentos!",
          uso: "Cera para polimentos, palha para artesanato, frutos para alimentação e madeira para construção.",
          beneficio: "A cera de carnaúba é biodegradável, atóxica e tem ponto de fusão muito alto (82°C).",
          cultural: "A carnaúba é símbolo do Ceará e é considerada a 'árvore da vida' por sua utilidade completa."
        },
        { 
          nome: "Aroeira", 
          desc: "Casca aromática, resina medicinal e uma das madeiras mais duras da região.",
          solo: "Calcários, secos, pedregosos e bem drenados.",
          veneno: "A seiva e o pó da madeira podem causar graves alergias e dermatites.",
          ameacas: "Severamente ameaçada de extinção devido à exploração madeireira histórica.",
          tags: ["toxica", "ameacada"],
          emoji: "🌿",
          curiosidade: "A aroeira é tão resistente que sua madeira dura mais de 50 anos enterrada! É usada para fazer moirões de cerca.",
          uso: "Madeira para construção, postes, mourões, tanino, resina medicinal e paisagismo.",
          beneficio: "A resina tem propriedades anti-inflamatórias, cicatrizantes e antidiarreicas.",
          cultural: "A aroeira é citada em canções populares e é considerada uma das árvores mais importantes do sertão."
        },
        { 
          nome: "Mulungu", 
          desc: "Copa larga e belas flores alaranjadas. Sua casca possui propriedades calmantes.",
          solo: "Arenosos a franco-argilosos, tolerando períodos de seca.",
          veneno: "As sementes são altamente tóxicas se ingeridas.",
          tags: ["toxica"],
          emoji: "🌸",
          curiosidade: "O mulungu é conhecido como a 'árvore da calma' porque sua casca é usada como ansiolítico natural!",
          uso: "Medicinal (ansiedade, insônia), madeira leve para artesanato e sombreamento.",
          beneficio: "A casca contém alcaloides com efeito calmante, similar a ansiolíticos naturais.",
          cultural: "O mulungu é reverenciado em rituais indígenas e é símbolo de paz e tranquilidade."
        },
        { 
          nome: "Angico", 
          desc: "Árvore rica em taninos. Sua casca é muito utilizada para curtume de couro e forragem.",
          solo: "Arenosos, profundos e de rápida drenagem.",
          veneno: "As sementes e brotos jovens podem conter compostos tóxicos para o gado.",
          ameacas: "Corte seletivo para obtenção de madeira e tanino.",
          tags: ["toxica", "ameacada"],
          emoji: "🌳",
          curiosidade: "O angico tem uma casca tão rica em tanino que pode tingir tecidos de tons marrons e pretos!",
          uso: "Curtume de couro, tintura natural, forragem, madeira e mel medicinal.",
          beneficio: "O mel de angico é famoso por seu sabor forte e propriedades medicinais.",
          cultural: "O angico é conhecido como o 'curtume da natureza' e é essencial na produção de couro artesanal."
        },
        { 
          nome: "Pau-ferro", 
          desc: "Árvore de madeira pesada, tronco marmorizado e flores roxas.",
          solo: "Argilosos ou arenosos profundos, adaptando-se bem a terrenos pedregosos.",
          veneno: "Não tóxica. Muito usada na medicina popular.",
          ameacas: "Uso comercial excessivo de sua madeira para marcenaria pesada.",
          tags: ["segura", "ameacada"],
          emoji: "🌳",
          curiosidade: "A madeira do pau-ferro é tão pesada que afunda na água! É uma das madeiras mais densas do Brasil.",
          uso: "Marcenaria fina, instrumentos musicais, cabos de ferramentas, paisagismo e medicina.",
          beneficio: "A casca é usada para tratar bronquite, asma e inflamações.",
          cultural: "O pau-ferro é símbolo de força e resistência, sendo muito presente na cultura popular nordestina."
        },
        { 
          nome: "Jurema-preta", 
          desc: "Espécie sagrada, com casca e raízes utilizadas em rituais tradicionais do Nordeste.",
          solo: "Arenosos, ácidos e de baixa fertilidade.",
          veneno: "Contem alcaloides psicoativos (DMT) concentrados na casca da raiz.",
          ameacas: "Exploração ilegal de lenha e avanço da pecuária extensiva.",
          tags: ["toxica", "ameacada"],
          emoji: "🌿",
          curiosidade: "A jurema-preta era usada pelos indígenas para rituais de cura e visão espiritual!",
          uso: "Rituais religiosos, medicina tradicional, forragem e madeira.",
          beneficio: "Usada em rituais para promover visões e conexão espiritual.",
          cultural: "A jurema-preta é sagrada para diversas religiões afro-indígenas do Nordeste."
        },
        { 
          nome: "Cajueiro", 
          desc: "Famoso pela castanha e pelo pseudofruto carnudo, suculento e doce.",
          solo: "Arenosos, profundos, leves e bem drenados.",
          veneno: "A casca da castanha crua contém líquido altamente corrosivo (LCC).",
          ameacas: "Nenhuma ameaça imediata devido ao cultivo comercial massivo.",
          tags: ["toxica"],
          emoji: "🥜",
          curiosidade: "O caju é um pseudofruto! A parte que comemos é o pedúnculo floral, e a castanha é o fruto verdadeiro.",
          uso: "Sucos, doces, castanhas torradas, óleo industrial e medicamentos.",
          beneficio: "O caju é rico em vitamina C, ferro, cálcio e antioxidantes.",
          cultural: "O caju é símbolo do Nordeste brasileiro, especialmente do Ceará."
        },
        { 
          nome: "Mangabeira", 
          desc: "Arbusto que produz látex para borracha e fruto doce apreciado na culinária.",
          solo: "Arenosos, ácidos e de baixíssima fertilidade (tabuleiros).",
          veneno: "O fruto verde contém látex que pode travar a boca, mas não é venenoso.",
          ameacas: "Especulação imobiliária em áreas litorâneas e expansão de pastos.",
          tags: ["segura"],
          emoji: "🍈",
          curiosidade: "A mangaba é uma das frutas mais ricas em vitamina C do mundo, superando a laranja!",
          uso: "Sucos, sorvetes, geleias, doces e látex para borracha.",
          beneficio: "Rica em vitamina C, ferro, fósforo e cálcio. Fortalece o sistema imunológico.",
          cultural: "A mangaba é muito presente no folclore e na culinária do litoral nordestino."
        },
        { 
          nome: "Jenipapo", 
          desc: "Fruto comestível cuja polpa verde-escura é usada para fazer tinta azul duradoura.",
          solo: "Profundos, férteis e com boa umidade.",
          veneno: "Livre de toxicidade.",
          ameacas: "Substituição de florestas ripárias por agricultura irrigada.",
          tags: ["segura"],
          emoji: "🍈",
          curiosidade: "O jenipapo produz uma tinta azul tão resistente que os indígenas a usavam para pintar o corpo de forma permanente!",
          uso: "Tintura corporal, sucos, licores, doces e artesanato.",
          beneficio: "Rico em ferro, cálcio, fósforo e vitaminas do complexo B.",
          cultural: "O jenipapo é sagrado para várias tribos indígenas, usado em rituais de passagem."
        },
        { 
          nome: "Graviola", 
          desc: "Fruto grande, de polpa branca, fibrosa, usada para sucos e doces.",
          solo: "Arenosos a argilosos, profundos e bem drenados.",
          veneno: "Sementes contêm compostos neurotóxicos leves.",
          ameacas: "Nenhuma ameaça imediata de extinção.",
          tags: ["toxica"],
          emoji: "🍈",
          curiosidade: "Estudos indicam que a graviola tem propriedades anticancerígenas, sendo estudada em várias universidades!",
          uso: "Sucos, doces, vitaminas, sorvetes e medicina alternativa.",
          beneficio: "Rica em antioxidantes, vitamina C, fibras e compostos bioativos.",
          cultural: "A graviola é considerada uma 'fruta milagrosa' na medicina popular caribenha."
        },
        { 
          nome: "Pitanga", 
          desc: "Frutinha vermelha e brilhante, extremamente rica em antioxidantes.",
          solo: "Férteis, úmidos e ricos em matéria orgânica.",
          veneno: "Não tóxica.",
          ameacas: "Urbanização de áreas de mata nativa.",
          tags: ["segura"],
          emoji: "🍒",
          curiosidade: "A pitanga tem 7 vezes mais vitamina C que a laranja! É uma das frutas mais antioxidantes do Brasil.",
          uso: "Sucos, geleias, licores, sorvetes e medicinal.",
          beneficio: "Fonte de vitamina A, C, ferro, cálcio e fósforo. Anti-inflamatória natural.",
          cultural: "A pitanga é muito presente nos quintais nordestinos e na culinária caseira."
        },
        { 
          nome: "Acerola", 
          desc: "Pequeno fruto originário das Antilhas, perfeitamente adaptado ao semiárido nordestino.",
          solo: "Arenosos e argilo-arenosos, bem drenados.",
          veneno: "Completamente segura e saudável.",
          ameacas: "Nenhuma; amplamente cultivada.",
          tags: ["segura"],
          emoji: "🍒",
          curiosidade: "A acerola tem até 80 vezes mais vitamina C que o limão! É a fruta mais rica em vitamina C do mundo.",
          uso: "Sucos, vitaminas, sorvetes, geleias, cosméticos e suplementos.",
          beneficio: "Fonte riquíssima de vitamina C, antioxidantes, ferro e cálcio.",
          cultural: "A acerola é conhecida como a 'fruta da saúde' e é muito consumida no Nordeste."
        },
        { 
          nome: "Goiabeira", 
          desc: "Árvore de casca lisa e frutos doces de polpa vermelha ou branca.",
          solo: "Diversos, adaptando-se bem a solos pobres desde que bem drenados.",
          veneno: "Não tóxica.",
          ameacas: "Nenhuma ameaça; espécie invasora em algumas áreas.",
          tags: ["segura"],
          emoji: "🍐",
          curiosidade: "A goiaba tem tanto licopeno quanto o tomate! É uma fruta coração-vermelho natural.",
          uso: "Consumo in natura, doces, geleias, sucos e vitaminas.",
          beneficio: "Rica em vitamina C, licopeno, fibras, potássio e vitaminas do complexo B.",
          cultural: "A goiaba é uma das frutas mais tradicionais do Brasil, presente em doces caseiros e festas juninas."
        },
        { 
          nome: "Tamarindeiro", 
          desc: "Vagem exótica adaptada com polpa marrom, extremamente ácida e fibrosa.",
          solo: "Arenosos, profundos e tolerantes à salinidade.",
          veneno: "Não tóxico.",
          ameacas: "Substituição por cultivos de maior retorno comercial rápido.",
          tags: ["segura"],
          emoji: "🌳",
          curiosidade: "O tamarindo é tão ácido que era usado pelos marinheiros para combater o escorbuto!",
          uso: "Sucos, doces, molhos, medicina tradicional e conservas.",
          beneficio: "Rico em vitaminas A, C, ácido tartárico, potássio e fibras.",
          cultural: "O tamarindo é muito usado na culinária indiana e foi trazido para o Brasil pelos portugueses."
        },
        { 
          nome: "Coqueiro", 
          desc: "Introduzido e amplamente naturalizado, famoso por sua água refrescante e polpa nutritiva.",
          solo: "Arenosos litorâneos e de dunas.",
          veneno: "Livre de toxicidade.",
          ameacas: "Pragas agrícolas como o ácaro-da-necrose e brocas do coqueiro.",
          tags: ["segura"],
          emoji: "🥥",
          curiosidade: "O coco não é uma noz, mas uma drupa! A água de coco já foi usada como soro fisiológico na Segunda Guerra Mundial.",
          uso: "Água de coco, leite, óleo, polpa, fibra para cordas e artesanato.",
          beneficio: "Água de coco é isotônica natural, rica em potássio e minerais essenciais.",
          cultural: "O coqueiro é símbolo das praias nordestinas e está presente em todas as manifestações culturais do litoral."
        },
        { 
          nome: "Babassu", 
          desc: "Palmeira imponente cujas amêndoas produzem um óleo versátil de grande uso doméstico.",
          solo: "Argilosos, ricos em matéria orgânica e úmidos.",
          veneno: "Não apresenta toxicidade.",
          ameacas: "Avanço do agronegócio e perda de direitos de comunidades tradicionais.",
          tags: ["segura", "ameacada"],
          emoji: "🌴",
          curiosidade: "O babassu é chamado de 'árvore do povo' porque é a base econômica de muitas comunidades tradicionais, especialmente as quebradeiras de coco!",
          uso: "Óleo culinário, cosméticos, sabões, carvão, artesanato e forragem.",
          beneficio: "O óleo de babassu é rico em ácido láurico, com propriedades anti-inflamatórias e hidratantes.",
          cultural: "O babassu é símbolo da resistência das mulheres quebradeiras de coco do Maranhão."
        },
        { 
          nome: "Palma-forrageira", 
          desc: "Cacto essencial para manter o gado hidratado e alimentado na seca.",
          solo: "Arenosos, leves e fáceis de drenar.",
          veneno: "Segura. Frutos e brotos jovens são comestíveis.",
          ameacas: "A praga da cochonilha-do-carmim destrói lavouras inteiras.",
          tags: ["segura"],
          emoji: "🌵",
          curiosidade: "A palma forrageira é uma das plantas mais eficientes em usar água, precisando de apenas 1/10 da água de outras forrageiras!",
          uso: "Alimentação animal, consumo humano (brotos), cosméticos e medicamentos.",
          beneficio: "Rica em água, carboidratos, vitaminas e minerais. Excelente para hidratação animal.",
          cultural: "A palma é conhecida como o 'milagre do sertão' por salvar rebanhos em períodos de seca."
        },
        { 
          nome: "Sabiá", 
          desc: "Árvore muito resistente, com flores amarelas, ótima produtora de lenha e estacas.",
          solo: "Argilo-arenosos e pedregosos.",
          veneno: "Não tóxica.",
          ameacas: "Corte excessivo e sem controle de rotação florestal.",
          tags: ["segura"],
          emoji: "🌳",
          curiosidade: "O sabiá é tão resistente que suas estacas criam raízes mesmo em solo seco! É uma planta 'viva' que se multiplica por estacas.",
          uso: "Lenha, cercas vivas, forragem, mel e paisagismo.",
          beneficio: "A madeira é excelente para combustível e as flores são muito visitadas por abelhas.",
          cultural: "O sabiá é uma das árvores mais queridas do sertão, símbolo de resistência e adaptação."
        },
        { 
          nome: "Pau-d'arco", 
          desc: "Também conhecido como ipê; possui madeira nobre e casca medicinal.",
          solo: "Férteis, profundos e bem drenados.",
          veneno: "Não tóxico.",
          ameacas: "Exploração ilegal de madeira devido ao alto valor comercial.",
          tags: ["segura", "ameacada"],
          emoji: "🌸",
          curiosidade: "O pau-d'arco é um dos maiores espetáculos da natureza! Suas flores rosa ou amarelas cobrem a árvore antes das folhas, criando um cenário mágico.",
          uso: "Madeira nobre para móveis, casca medicinal, paisagismo e extração de tanino.",
          beneficio: "A casca tem propriedades anti-inflamatórias, antifúngicas e cicatrizantes.",
          cultural: "O ipê (pau-d'arco) é a árvore símbolo do Brasil e representa a beleza e a força da nossa flora."
        },
        { 
          nome: "Pau-brasil", 
          desc: "Árvore histórica de madeira vermelha que deu origem ao nome do nosso país.",
          solo: "Argilo-arenosos e férteis de floresta estacional.",
          veneno: "Não tóxica.",
          ameacas: "Altamente ameaçada de extinção na natureza.",
          tags: ["segura", "ameacada"],
          emoji: "🌳",
          curiosidade: "O pau-brasil é a árvore que deu nome ao nosso país! Sua madeira rendia um corante vermelho tão valioso que os índios trocavam por espelhos e quinquilharias.",
          uso: "Madeira para móveis, corante, instrumentos musicais e paisagismo.",
          beneficio: "A madeira é densa e durável, com alto valor comercial.",
          cultural: "O pau-brasil é símbolo nacional e está representado em nossa bandeira, com a estrela da constelação do Cruzeiro."
        },
        { 
          nome: "Jacarandá", 
          desc: "Árvore ornamental magnífica de flores roxas ou azuladas e madeira nobre.",
          solo: "Férteis, profundos e bem drenados.",
          veneno: "Não tóxico.",
          ameacas: "Exploração excessiva da madeira fina para móveis e instrumentos.",
          tags: ["segura", "ameacada"],
          emoji: "🌸",
          curiosidade: "O jacarandá é uma das madeiras mais nobres e valiosas do mundo, usada em instrumentos musicais de altíssima qualidade!",
          uso: "Móveis finos, instrumentos musicais, esculturas, paisagismo e medicina popular.",
          beneficio: "A madeira é durável, resistente a cupins e tem um aroma agradável.",
          cultural: "O jacarandá é símbolo de elegância e requinte, presente em casarões históricos e igrejas barrocas."
        },
        { 
          nome: "Cedro", 
          desc: "Madeira nobre e aromática que repele insetos naturalmente.",
          solo: "Férteis, profundos e bem drenados.",
          veneno: "Não tóxico.",
          ameacas: "Exploração de madeira de lei sem plano de manejo sustentável.",
          tags: ["segura", "ameacada"],
          emoji: "🌳",
          curiosidade: "O cedro é uma madeira tão aromática que repele mariposas e traças naturalmente! Por isso é usado em baús e guarda-roupas.",
          uso: "Marcenaria, construção naval, móveis, instrumentos musicais e extração de óleo essencial.",
          beneficio: "O óleo de cedro tem propriedades calmantes, repelentes e anti-inflamatórias.",
          cultural: "O cedro era usado pelos fenícios para construir seus navios e pelos egípcios para mumificar faraós."
        },
        { 
          nome: "Ingazeira", 
          desc: "Árvore de margem de rio que produz vagens com sementes envoltas em polpa doce.",
          solo: "Úmidos, aluviais e próximos a córregos.",
          veneno: "Livre de toxicidade.",
          ameacas: "Retirada de matas ciliares e poluição de rios.",
          tags: ["segura"],
          emoji: "🌳",
          curiosidade: "A ingazeira é uma árvore 'amiga da água'! Suas raízes ajudam a proteger as margens dos rios contra a erosão.",
          uso: "Sombreamento, recuperação de áreas degradadas, forragem e artesanato.",
          beneficio: "A polpa das sementes é doce e nutritiva, consumida por animais e pessoas.",
          cultural: "A ingazeira é importante para a preservação dos rios e é conhecida como a 'mãe das águas'."
        }
      ];

      let filtroAtivo = 'todas';
      let termoBusca = '';

      document.getElementById('count-todas').innerText = especies.length;

      function render() {
        const grid = document.getElementById('plantaGrid');
        const emptyState = document.getElementById('emptyState');
        if (!grid) return;

        const filtradas = especies.filter(planta => {
          const matchBusca = planta.nome.toLowerCase().includes(termoBusca.toLowerCase()) || 
                             planta.desc.toLowerCase().includes(termoBusca.toLowerCase()) ||
                             planta.solo.toLowerCase().includes(termoBusca.toLowerCase());
          
          if (filtroAtivo === 'todas') return matchBusca;
          return matchBusca && planta.tags.includes(filtroAtivo);
        });

        if (filtradas.length === 0) {
          grid.classList.add('hidden');
          emptyState.classList.remove('hidden');
          document.getElementById('contadorExibido').innerText = '0';
          return;
        } else {
          grid.classList.remove('hidden');
          emptyState.classList.add('hidden');
        }

        document.getElementById('contadorExibido').innerText = filtradas.length;

        let html = '';
        filtradas.forEach((planta) => {
          const eAmeacada = planta.tags.includes('ameacada');
          const eToxica = planta.tags.includes('toxica');
          const eAgricola = planta.tags.includes('agricola');
          
          let cardBorderClass = "border-stone-200/80 hover:border-caatinga-400";
          
          if (eAgricola) {
            cardBorderClass = "border-agricola-100 hover:border-agricola-500 bg-gradient-to-br from-white to-amber-50/10";
          } else if (eAmeacada) {
            cardBorderClass = "border-amber-200/80 hover:border-amber-400";
          } else if (eToxica) {
            cardBorderClass = "border-red-200/60 hover:border-red-400";
          }

          const idGlobal = especies.findIndex(item => item.nome === planta.nome);

          html += `
            <div onclick="abrirModal(${idGlobal})" class="card bg-white rounded-[2.25rem] p-6 shadow-sm hover:shadow-xl hover:-translate-y-1 transition-all duration-300 flex flex-col justify-between border ${cardBorderClass} cursor-pointer group">
              <div>
                <div class="flex justify-between items-start mb-2">
                  <span class="emoji-big">${planta.emoji}</span>
                  <div class="flex flex-col gap-1 items-end">
                    ${eAgricola ? '<span class="text-[9px] font-extrabold uppercase tracking-wider px-2 py-0.5 rounded-md bg-amber-100 text-amber-800 border border-amber-200/40">🌾 Lavoura</span>' : ''}
                    ${eAmeacada ? '<span class="text-[9px] font-extrabold uppercase tracking-wider px-2 py-0.5 rounded-md bg-amber-50 text-amber-700 border border-amber-200/40">⚠️ Ameaçada</span>' : ''}
                    ${eToxica ? '<span class="text-[9px] font-extrabold uppercase tracking-wider px-2 py-0.5 rounded-md bg-red-50 text-red-700 border border-red-200/30">⚠️ Alerta</span>' : ''}
                  </div>
                </div>

                <h3 class="font-serif text-xl font-bold text-stone-900 mb-2 tracking-tight group-hover:text-caatinga-700 transition-colors">
                  ${planta.nome}
                </h3>
                <p class="text-xs text-stone-500 leading-relaxed font-medium mb-3 italic line-clamp-2">
                  "${planta.desc}"
                </p>
                <span class="inline-flex items-center text-[10px] text-caatinga-600 font-bold group-hover:translate-x-1 transition-transform">
                  Descobrir segredos &rarr;
                </span>
              </div>
              
              <div class="space-y-3 pt-4 mt-4 border-t border-dashed border-stone-100 pointer-events-none">
                <div class="text-[11px] bg-stone-50 p-2.5 rounded-xl border border-stone-100/50">
                  <strong class="block text-[9px] uppercase tracking-wider text-caatinga-700 mb-0.5">🌱 Solo</strong>
                  <span class="text-stone-600 font-medium truncate block">${planta.solo}</span>
                </div>
              </div>
            </div>
          `;
        });

        grid.innerHTML = html;
      }

      window.abrirModal = function(id) {
        const planta = especies[id];
        const modal = document.getElementById('plantaModal');
        
        document.getElementById('modalEmoji').innerText = planta.emoji;
        document.getElementById('modalNome').innerText = planta.nome;
        document.getElementById('modalDesc').innerText = `"${planta.desc}"`;
        
        // Informações únicas
        document.getElementById('modalCuriosidade').innerText = planta.curiosidade || "Esta planta guarda segredos fascinantes do sertão!";
        document.getElementById('modalUso').innerText = planta.uso || "Usos diversos na cultura e economia local.";
        document.getElementById('modalBeneficio').innerText = planta.beneficio || "Contribui para a saúde e bem-estar das comunidades.";
        document.getElementById('modalCultural').innerText = planta.cultural || "Faz parte da identidade e tradição do povo nordestino.";
        
        document.getElementById('modalSolo').innerText = planta.solo;
        document.getElementById('modalVeneno').innerText = planta.veneno;
        document.getElementById('modalAmeacas').innerText = `🔥 ${planta.ameacas || "Sem ameaças críticas reportadas."}`;

        // Tags personalizadas
        const tagsContainer = document.getElementById('modalTags');
        tagsContainer.innerHTML = '';
        const tagMap = {
          'agricola': { class: 'industrial', label: '🌾 Agrícola' },
          'segura': { class: 'alimenticio', label: '🍎 Comestível' },
          'toxica': { class: 'perigo', label: '⚠️ Tóxica' },
          'ameacada': { class: 'artesanato', label: '🔥 Ameaçada' }
        };
        planta.tags.forEach(tag => {
          if (tagMap[tag]) {
            const span = document.createElement('span');
            span.className = `info-tag ${tagMap[tag].class}`;
            span.textContent = tagMap[tag].label;
            tagsContainer.appendChild(span);
          }
        });

        modal.classList.remove('hidden');
        setTimeout(() => {
          modal.classList.remove('opacity-0');
          modal.firstElementChild.classList.remove('scale-95');
        }, 10);
      };

      window.fecharModal = function() {
        const modal = document.getElementById('plantaModal');
        modal.classList.add('opacity-0');
        modal.firstElementChild.classList.add('scale-95');
        setTimeout(() => {
          modal.classList.add('hidden');
        }, 300);
      };

      document.getElementById('plantaModal').addEventListener('click', function(e) {
        if (e.target === this) {
          fecharModal();
        }
      });

      window.filtrarEspesies = function(categoria) {
        filtroAtivo = categoria;
        
        document.querySelectorAll('.btn-filtro').forEach(btn => {
          btn.className = "btn-filtro px-4 py-2.5 rounded-xl text-xs font-semibold transition-all bg-stone-100 text-stone-600 hover:bg-stone-200/70 border border-stone-200/50";
        });

        const activeBtn = document.getElementById(`btn-${categoria}`);
        if (activeBtn) {
          if (categoria === 'todas') {
            activeBtn.className = "btn-filtro px-4 py-2.5 rounded-xl text-xs font-semibold transition-all bg-caatinga-800 text-white shadow-sm";
          } else if (categoria === 'agricola') {
            activeBtn.className = "btn-filtro px-4 py-2.5 rounded-xl text-xs font-semibold transition-all bg-amber-500 text-white shadow-sm";
          } else if (categoria === 'toxicas') {
            activeBtn.className = "btn-filtro px-4 py-2.5 rounded-xl text-xs font-semibold transition-all bg-red-600 text-white shadow-sm";
          } else if (categoria === 'ameacadas') {
            activeBtn.className = "btn-filtro px-4 py-2.5 rounded-xl text-xs font-semibold transition-all bg-amber-700 text-white shadow-sm";
          } else {
            activeBtn.className = "btn-filtro px-4 py-2.5 rounded-xl text-xs font-semibold transition-all bg-caatinga-600 text-white shadow-sm";
          }
        }

        render();
      };

      document.getElementById('searchInput').addEventListener('input', (e) => {
        termoBusca = e.target.value;
        render();
      });

      render();
    })();
  </script>
</body>
</html>
