# KALEBE-XAVIER-REIS
DEI ET PATRIS DISCIPULADO 
import React, { useState, useEffect } from 'react';
import { 
  Home, BookOpen, Users, Flame, CheckCircle, Send, Heart, 
  Menu, X, ChevronRight, Trophy, Calendar, Book, Mic, ArrowLeft, Share2
} from 'lucide-react';

// --- CONFIGURAÇÕES GLOBAIS ---
const COLORS = {
  gold: '#C59D5F',
  goldLight: '#E5C585',
  dark: '#0F0F0F',
  darkGray: '#1A1A1A',
  accent: '#8B0000',
  white: '#E0E0E0'
};

const MODULES_DATA = [
  {
    id: 1,
    title: "Evangelizar",
    subtitle: "O Grito no Deserto",
    icon: <Flame size={24} />,
    content: "O século 21 grita em nossos ouvidos. Notificações, likes, a pressão estética... Mas no silêncio do seu quarto, quem é você? O primeiro passo não é sobre religião, é sobre sobrevivência da alma. Evangelizar é apresentar a única pessoa capaz de preencher o abismo: Jesus Cristo. A estratégia 'Paz e Bem' de São Francisco nos ensina a evangelizar com a vida."
  },
  {
    id: 2,
    title: "Comunidade",
    subtitle: "O Abraço de Deus",
    icon: <Users size={24} />,
    content: "O mundo virtual promete conexão, mas entrega solidão. Santo Agostinho descobriu que fora de Deus não há descanso. A 'Célula Católica' é o útero onde a fé é gestada. No Grupo de Jovens São João Batista, ninguém fica para trás. A depressão e o medo se dissolvem quando estamos unidos no Corpo Místico de Cristo."
  },
  {
    id: 3,
    title: "Treinar",
    subtitle: "A Pequena Via",
    icon: <BookOpen size={24} />,
    content: "Santa Teresinha do Menino Jesus nos ensina o segredo da santidade moderna: a Pequena Via. Você não precisa fazer milagres grandiosos. Precisa fazer as pequenas coisas com um GRANDE AMOR. Treinar é esvaziar-se de si mesmo para ser cheio de Deus."
  },
  {
    id: 4,
    title: "Missão",
    subtitle: "Santidade de Tênis",
    icon: <Trophy size={24} />,
    content: "Carlo Acutis provou: é possível ser jovem, amar computadores e ser SANTO. O missionário carrega um notebook numa mão e o Terço na outra. A internet é o novo continente a ser evangelizado. Não aceite ser uma fotocópia. Deus te desenhou original!"
  }
];

// --- COMPONENTE PRINCIPAL ---
export default function App() {
  const [activeTab, setActiveTab] = useState('inicio');
  const [showSplash, setShowSplash] = useState(true);

  // Splash Screen
  useEffect(() => {
    const timer = setTimeout(() => setShowSplash(false), 2500);
    return () => clearTimeout(timer);
  }, []);

  if (showSplash) {
    return (
      <div className="h-screen w-full flex flex-col items-center justify-center bg-[#0F0F0F] text-[#C59D5F] animate-pulse">
        <div className="w-24 h-24 rounded-full border-4 border-[#C59D5F] flex items-center justify-center mb-4 shadow-[0_0_30px_rgba(197,157,95,0.3)]">
          <Flame size={48} />
        </div>
        <h1 className="font-serif text-2xl font-bold tracking-widest">DEI ET PATRIS</h1>
        <p className="text-xs uppercase tracking-widest mt-2 text-gray-500">Canutama - AM</p>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-[#0F0F0F] text-[#E0E0E0] font-sans pb-24 relative overflow-hidden">
      {/* Header Fixo */}
      <header className="fixed top-0 w-full z-50 bg-[#0F0F0F]/95 backdrop-blur-md border-b border-[#C59D5F]/20 px-4 py-3 flex justify-between items-center shadow-lg">
        <div className="flex items-center gap-2">
          <div className="w-8 h-8 rounded-full border border-[#C59D5F] overflow-hidden bg-black flex items-center justify-center">
             <Flame size={16} color={COLORS.gold} />
          </div>
          <span className="font-serif font-bold text-[#C59D5F] text-sm tracking-wider">DEI ET PATRIS</span>
        </div>
        <button className="text-[#C59D5F] p-2 rounded-full hover:bg-[#1A1A1A]">
          <Heart size={20} className="text-red-600" fill="#dc2626" />
        </button>
      </header>

      {/* Conteúdo Principal */}
      <main className="pt-20 px-4">
        {activeTab === 'inicio' && <HomeView setActiveTab={setActiveTab} />}
        {activeTab === 'liturgia' && <LiturgyView />}
        {activeTab === 'estudo' && <StudyView />}
        {activeTab === 'comunidade' && <CommunityView />}
        {activeTab === 'perfil' && <ProfileView />}
      </main>

      {/* Navegação Inferior (5 Botões) */}
      <nav className="fixed bottom-0 w-full bg-[#1A1A1A] border-t border-[#C59D5F]/20 py-2 px-2 flex justify-between items-end z-50">
        <NavItem icon={<Home size={20} />} label="Início" isActive={activeTab === 'inicio'} onClick={() => setActiveTab('inicio')} />
        <NavItem icon={<Book size={20} />} label="Liturgia" isActive={activeTab === 'liturgia'} onClick={() => setActiveTab('liturgia')} />
        
        {/* Botão Central Destacado - FORMAÇÃO/ESTUDO */}
        <div className="relative -top-4 mx-2">
          <button 
            onClick={() => setActiveTab('estudo')}
            className={`w-16 h-16 rounded-full flex flex-col items-center justify-center border-4 border-[#0F0F0F] shadow-[0_0_20px_rgba(197,157,95,0.3)] transition-transform ${activeTab === 'estudo' ? 'bg-[#E5C585] scale-110 text-black' : 'bg-[#C59D5F] text-[#0F0F0F]'}`}
          >
            <Flame size={28} fill={activeTab === 'estudo' ? 'black' : '#0F0F0F'} />
            <span className="text-[9px] font-bold mt-0.5">ESTUDO</span>
          </button>
        </div>

        <NavItem icon={<Users size={20} />} label="Mural" isActive={activeTab === 'comunidade'} onClick={() => setActiveTab('comunidade')} />
        <NavItem icon={<Trophy size={20} />} label="Missão" isActive={activeTab === 'perfil'} onClick={() => setActiveTab('perfil')} />
      </nav>
    </div>
  );
}

// --- VIEW: INÍCIO ---
function HomeView({ setActiveTab }) {
  return (
    <div className="space-y-6 animate-fade-in-up">
      {/* Banner Principal */}
      <div className="relative rounded-2xl overflow-hidden p-6 text-center border border-[#C59D5F]/30 shadow-lg group">
        <div className="absolute inset-0 z-0">
          <img 
            src="https://images.unsplash.com/photo-1511632765486-a01980e01a18?q=80&w=2070&auto=format&fit=crop" 
            alt="Background" 
            className="w-full h-full object-cover opacity-30 group-hover:scale-105 transition duration-700" 
          />
          <div className="absolute inset-0 bg-gradient-to-b from-transparent via-[#0F0F0F]/50 to-[#0F0F0F]"></div>
        </div>
        
        <div className="relative z-10">
          <h2 className="text-[#C59D5F] tracking-widest text-xs uppercase mb-2">Canutama - AM</h2>
          <h1 className="text-2xl font-serif font-bold text-white mb-4 leading-tight">
            Seja um Discípulo <br/><span className="text-[#C59D5F]">Radical</span>
          </h1>
          <button 
            onClick={() => setActiveTab('estudo')}
            className="bg-[#C59D5F] text-[#0F0F0F] font-bold py-3 px-8 rounded-full text-sm hover:bg-white transition shadow-[0_0_15px_rgba(197,157,95,0.4)]"
          >
            Começar Treinamento
          </button>
        </div>
      </div>

      {/* Atalho Liturgia do Dia */}
      <div onClick={() => setActiveTab('liturgia')} className="bg-[#1A1A1A] p-5 rounded-xl border-l-4 border-[#C59D5F] cursor-pointer hover:bg-[#252525] transition">
        <div className="flex justify-between items-start">
          <div>
            <h3 className="text-[#C59D5F] font-bold text-sm flex items-center gap-2">
              <BookOpen size={16} /> Evangelho de Hoje
            </h3>
            <p className="text-lg font-serif mt-1">São Lucas 10, 1-9</p>
          </div>
          <ChevronRight className="text-gray-600" size={20}/>
        </div>
        <p className="text-sm text-gray-400 italic mt-2 line-clamp-2">"A colheita é grande, mas os trabalhadores são poucos. Pedi, pois, ao Senhor da colheita..."</p>
      </div>

      {/* Cards de Acesso Rápido */}
      <div className="grid grid-cols-2 gap-4">
        <QuickCard 
          icon={<Trophy size={24} className="text-[#C59D5F]" />} 
          title="Desafio Semanal" 
          desc="Adoração Eucarística"
          onClick={() => setActiveTab('perfil')}
        />
        <QuickCard 
          icon={<Heart size={24} className="text-[#8B0000]" />} 
          title="Pedidos de Oração" 
          desc="Interceda agora"
          onClick={() => setActiveTab('comunidade')}
        />
      </div>
    </div>
  );
}

// --- VIEW: LITURGIA E HOMILIA (NOVA) ---
function LiturgyView() {
  const [readingTab, setReadingTab] = useState('evangelho'); // 'primeira', 'salmo', 'evangelho', 'homilia'

  const readings = {
    primeira: {
      ref: "Leitura da Carta de São Paulo aos Romanos (8, 12-17)",
      text: "Irmãos: Não somos devedores à carne, para vivermos segundo a carne. Pois, se viverdes segundo a carne, morrereis; mas, se pelo Espírito fizerdes morrer as obras do corpo, vivereis. Todos aqueles que são conduzidos pelo Espírito de Deus são filhos de Deus..."
    },
    salmo: {
      ref: "Salmo 67 (68)",
      title: "O nosso Deus é um Deus que salva.",
      text: "Levanta-se Deus e dispersam-se os seus inimigos,\ne fogem diante dele os que o odeiam.\nMas os justos se alegram na presença de Deus,\nrejubilam de alegria e o exaltam."
    },
    evangelho: {
      ref: "Proclamação do Evangelho de Jesus Cristo segundo Lucas (13, 10-17)",
      text: "Naquele tempo, Jesus estava ensinando numa sinagoga em dia de sábado. Havia lá uma mulher que, há dezoito anos, estava com um espírito que a tornava doente. Ela era encurvada e incapaz de se endireitar. Vendo-a, Jesus a chamou e lhe disse: 'Mulher, estás livre da tua doença'."
    },
    homilia: {
      title: "A Cura que Endireita a Vida",
      author: "Reflexão Dei et Patris",
      text: "Muitos jovens hoje andam 'encurvados' espiritualmente. Olham apenas para o chão, para a tela do celular, para os próprios problemas. O pecado nos encurva, nos fecha em nós mesmos. Jesus, hoje, nos chama na sinagoga (na Igreja, no Grupo de Jovens) para nos tocar. Ele quer que você olhe para o Alto! A missão do jovem cristão é andar de cabeça erguida, não por orgulho, mas pela dignidade de ser filho de Deus."
    }
  };

  return (
    <div className="space-y-4 pb-20 animate-fade-in-up h-full flex flex-col">
      {/* Header Liturgia */}
      <div className="flex justify-between items-center pb-2 border-b border-[#C59D5F]/20">
        <div>
          <h2 className="text-2xl font-serif font-bold text-white">Liturgia Diária</h2>
          <p className="text-[#C59D5F] text-xs uppercase tracking-widest">Terça-feira, 23ª Semana TC</p>
        </div>
        <Calendar size={24} className="text-[#C59D5F]" />
      </div>

      {/* Tabs de Leitura */}
      <div className="flex gap-2 overflow-x-auto pb-2 scrollbar-hide">
        <LiturgyTab label="1ª Leitura" active={readingTab === 'primeira'} onClick={() => setReadingTab('primeira')} />
        <LiturgyTab label="Salmo" active={readingTab === 'salmo'} onClick={() => setReadingTab('salmo')} />
        <LiturgyTab label="Evangelho" active={readingTab === 'evangelho'} onClick={() => setReadingTab('evangelho')} />
        <LiturgyTab label="Homilia" active={readingTab === 'homilia'} onClick={() => setReadingTab('homilia')} isSpecial />
      </div>

      {/* Conteúdo da Leitura */}
      <div className="flex-1 bg-[#1A1A1A] rounded-xl p-6 overflow-y-auto border border-gray-800 relative">
        {readingTab === 'homilia' ? (
          // Layout Especial para Homilia
          <div className="space-y-4">
            <div className="flex items-center justify-between">
               <span className="bg-[#C59D5F]/20 text-[#C59D5F] px-3 py-1 rounded-full text-xs font-bold">Reflexão do Dia</span>
               <button className="text-gray-400 hover:text-white"><Share2 size={20}/></button>
            </div>
            <h3 className="text-xl font-serif font-bold text-white">{readings.homilia.title}</h3>
            <p className="text-gray-500 text-xs mb-4">Por {readings.homilia.author}</p>
            
            <div className="bg-[#0F0F0F] p-4 rounded-lg border border-[#C59D5F]/20 flex items-center gap-4 mb-4">
               <div className="bg-[#C59D5F] p-3 rounded-full text-black"><Mic size={20} /></div>
               <div>
                 <p className="text-xs text-gray-400">Ouvir Homilia</p>
                 <div className="h-1 w-32 bg-gray-700 rounded-full mt-1 overflow-hidden">
                   <div className="h-full bg-[#C59D5F] w-1/3"></div>
                 </div>
               </div>
            </div>

            <p className="text-gray-300 leading-relaxed text-justify font-serif text-lg">
              {readings.homilia.text}
            </p>
          </div>
        ) : (
          // Layout para Leituras Bíblicas
          <>
            <h3 className="text-[#C59D5F] font-bold text-sm mb-4 border-b border-gray-700 pb-2">
              {readings[readingTab].ref}
            </h3>
            {readingTab === 'salmo' && (
              <p className="text-red-400 text-sm italic mb-4 text-center border-l-2 border-red-900 pl-2">
                R. {readings.salmo.title}
              </p>
            )}
            <p className="text-gray-200 leading-8 text-lg font-serif text-justify">
              {readings[readingTab].text}
            </p>
            <div className="mt-8 text-center text-xs text-gray-500 uppercase tracking-widest">
              — Palavra do Senhor. <br/> 
              <span className="text-white font-bold text-sm">Graças a Deus.</span>
            </div>
          </>
        )}
      </div>
    </div>
  );
}

// --- VIEW: FORMAÇÃO/ESTUDO (A ESSÊNCIA) ---
function StudyView() {
  const [tasks, setTasks] = useState({ rosary: false, bible: false, mass: false, reading: false });
  const [selectedModule, setSelectedModule] = useState(null);

  const toggleTask = (task) => setTasks(prev => ({...prev, [task]: !prev[task]}));
  const progress = Object.values(tasks).filter(Boolean).length * 25;

  // Renderização detalhada de um módulo quando clicado
  if (selectedModule) {
    return (
      <div className="animate-fade-in-up pb-24">
        <button onClick={() => setSelectedModule(null)} className="flex items-center text-[#C59D5F] mb-4 text-sm font-bold">
          <ArrowLeft size={16} className="mr-2" /> Voltar para Trilha
        </button>
        <div className="bg-[#1A1A1A] p-6 rounded-2xl border border-[#C59D5F]/30">
          <div className="w-12 h-12 bg-[#C59D5F] rounded-full flex items-center justify-center text-black mb-4 shadow-lg shadow-[#C59D5F]/20">
            {selectedModule.icon}
          </div>
          <h2 className="text-3xl font-serif font-bold text-white mb-2">{selectedModule.title}</h2>
          <h3 className="text-[#C59D5F] text-lg mb-6 italic">{selectedModule.subtitle}</h3>
          <p className="text-gray-300 leading-loose text-justify text-lg border-t border-gray-800 pt-6">
            {selectedModule.content}
          </p>
          <button className="w-full mt-8 bg-[#C59D5F] text-black font-bold py-3 rounded-xl hover:bg-white transition">
            Marcar Como Estudado
          </button>
        </div>
      </div>
    );
  }

  // Visão Geral da Formação
  return (
    <div className="space-y-8 pb-20 animate-fade-in-up">
      {/* Header Progresso */}
      <div className="bg-gradient-to-r from-[#1A1A1A] to-[#0F0F0F] p-6 rounded-2xl border border-[#C59D5F]/20">
        <div className="flex justify-between items-end mb-4">
          <div>
            <h2 className="text-xl font-bold text-white">Minhas Metas</h2>
            <p className="text-xs text-gray-500">Santidade Diária</p>
          </div>
          <span className="text-[#C59D5F] text-2xl font-bold">{progress}%</span>
        </div>
        <div className="w-full bg-black rounded-full h-2">
          <div className="bg-[#C59D5F] h-2 rounded-full transition-all duration-500 shadow-[0_0_10px_#C59D5F]" style={{ width: `${progress}%` }}></div>
        </div>
        
        <div className="grid grid-cols-4 gap-2 mt-6">
          <MiniTask icon={<div className="text-[10px] font-bold">TERÇO</div>} active={tasks.rosary} onClick={() => toggleTask('rosary')} />
          <MiniTask icon={<BookOpen size={14}/>} active={tasks.bible} onClick={() => toggleTask('bible')} />
          <MiniTask icon={<Calendar size={14}/>} active={tasks.mass} onClick={() => toggleTask('mass')} />
          <MiniTask icon={<Flame size={14}/>} active={tasks.reading} onClick={() => toggleTask('reading')} />
        </div>
      </div>

      {/* Trilha de Discipulado (OS MÓDULOS) */}
      <div>
        <h3 className="text-lg font-serif font-bold text-white mb-4 pl-2 border-l-4 border-[#C59D5F]">
          Trilha de Discipulado
        </h3>
        <div className="grid gap-4">
          {MODULES_DATA.map((module, index) => (
            <div 
              key={module.id}
              onClick={() => setSelectedModule(module)}
              className="bg-[#1A1A1A] p-4 rounded-xl border border-gray-800 flex items-center justify-between hover:border-[#C59D5F] hover:bg-[#202020] transition cursor-pointer group"
            >
              <div className="flex items-center gap-4">
                <div className="text-gray-600 font-bold text-lg group-hover:text-[#C59D5F]">0{index + 1}</div>
                <div>
                  <h4 className="font-bold text-white">{module.title}</h4>
                  <p className="text-xs text-gray-500">{module.subtitle}</p>
                </div>
              </div>
              <ChevronRight size={20} className="text-gray-600 group-hover:text-[#C59D5F]" />
            </div>
          ))}
        </div>
      </div>
    </div>
  );
}

// --- VIEW: MURAL/COMUNIDADE ---
function CommunityView() {
  const [prayers, setPrayers] = useState([
    { id: 1, author: 'Maria S.', text: 'Pela saúde da minha avó e paz na família.', likes: 12 },
    { id: 2, author: 'João P.', text: 'Pelo discernimento vocacional dos jovens.', likes: 8 },
  ]);
  const [newPrayer, setNewPrayer] = useState("");

  const handlePost = () => {
    if (!newPrayer.trim()) return;
    setPrayers([{ id: Date.now(), author: 'Você', text: newPrayer, likes: 0 }, ...prayers]);
    setNewPrayer("");
  };

  return (
    <div className="space-y-6 pb-20 animate-fade-in-up">
      <h2 className="text-2xl font-serif font-bold text-white">Mural de Oração</h2>
      <div className="bg-[#1A1A1A] p-4 rounded-xl border border-[#C59D5F]/20">
        <textarea 
          value={newPrayer}
          onChange={(e) => setNewPrayer(e.target.value)}
          placeholder="Qual sua intenção para hoje?"
          className="w-full bg-[#0F0F0F] text-white p-3 rounded-lg text-sm border border-gray-800 focus:border-[#C59D5F] outline-none resize-none h-24"
        />
        <div className="flex justify-between items-center mt-3">
          <span className="text-xs text-gray-500">Sua oração será vista pelo grupo.</span>
          <button onClick={handlePost} className="bg-[#C59D5F] text-black px-4 py-2 rounded-full text-xs font-bold flex items-center gap-2 hover:bg-white transition">
            Enviar <Send size={14} />
          </button>
        </div>
      </div>

      <div className="space-y-4">
        {prayers.map(prayer => (
          <div key={prayer.id} className="bg-[#1A1A1A] p-4 rounded-xl border-l-2 border-[#8B0000]">
            <div className="flex justify-between items-start mb-2">
              <span className="font-bold text-[#C59D5F] text-sm">{prayer.author}</span>
              <span className="text-xs text-gray-600">há instantes</span>
            </div>
            <p className="text-gray-300 text-sm mb-3">{prayer.text}</p>
            <div className="flex items-center gap-2 text-gray-500 text-xs">
              <button className="flex items-center gap-1 hover:text-red-500 transition">
                <Heart size={14} /> Rezar por isso ({prayer.likes})
              </button>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}

// --- VIEW: PERFIL/MISSÃO ---
function ProfileView() {
  return (
    <div className="space-y-6 pb-20 animate-fade-in-up">
      <div className="flex items-center gap-4">
        <div className="w-20 h-20 rounded-full border-2 border-[#C59D5F] p-1">
          <div className="w-full h-full rounded-full bg-gray-800 flex items-center justify-center text-2xl">😎</div>
        </div>
        <div>
          <h2 className="text-xl font-bold text-white">Jovem Católico</h2>
          <p className="text-[#C59D5F] text-sm">Nível: Discípulo Iniciante</p>
        </div>
      </div>

      <div className="bg-gradient-to-r from-gray-900 to-gray-800 rounded-xl p-6 border border-[#C59D5F]/20 relative overflow-hidden">
        <div className="absolute top-0 right-0 p-3 opacity-10 text-[#C59D5F]">
           <Trophy size={80} />
        </div>
        <h3 className="text-lg font-serif font-bold text-white mb-2">Desafio Carlo Acutis</h3>
        <p className="text-sm text-gray-400 mb-4">"A Eucaristia é a minha autoestrada para o Céu."</p>
        
        <div className="space-y-3">
          <div className="flex items-center justify-between text-sm bg-black/40 p-3 rounded lg">
            <span className="text-gray-300">1. Participar da Missa Dominical</span>
            <CheckCircle size={18} className="text-green-500" />
          </div>
          <div className="flex items-center justify-between text-sm bg-black/40 p-3 rounded lg">
            <span className="text-gray-300">2. Adoração Eucarística (30min)</span>
            <div className="w-4 h-4 rounded-full border border-gray-500"></div>
          </div>
        </div>
      </div>
    </div>
  );
}

// --- COMPONENTES AUXILIARES ---

function NavItem({ icon, label, isActive, onClick }) {
  return (
    <button 
      onClick={onClick}
      className={`flex flex-col items-center justify-center w-14 pb-1 transition-colors duration-300 ${isActive ? 'text-[#C59D5F]' : 'text-gray-500 hover:text-gray-300'}`}
    >
      {icon}
      <span className="text-[9px] mt-1 font-medium">{label}</span>
    </button>
  );
}

function LiturgyTab({ label, active, onClick, isSpecial }) {
  return (
    <button 
      onClick={onClick}
      className={`whitespace-nowrap px-4 py-2 rounded-full text-xs font-bold transition-all ${
        active 
          ? isSpecial ? 'bg-red-900 text-white' : 'bg-[#C59D5F] text-black'
          : 'bg-[#1A1A1A] text-gray-400 border border-gray-800'
      }`}
    >
      {label}
    </button>
  )
}

function QuickCard({ icon, title, desc, onClick }) {
  return (
    <div onClick={onClick} className="bg-[#1A1A1A] p-4 rounded-xl border border-gray-800 hover:border-[#C59D5F]/50 transition cursor-pointer active:scale-95">
      <div className="mb-3">{icon}</div>
      <h3 className="font-bold text-white text-sm">{title}</h3>
      <p className="text-xs text-gray-500">{desc}</p>
    </div>
  );
}

function MiniTask({ icon, active, onClick }) {
  return (
    <button 
      onClick={onClick}
      className={`h-12 rounded-lg flex items-center justify-center border transition-all ${active ? 'bg-[#C59D5F] text-black border-[#C59D5F]' : 'bg-[#0F0F0F] text-gray-500 border-gray-800'}`}
    >
      {icon}
    </button>
  )
}


