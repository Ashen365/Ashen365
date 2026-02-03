import { useState, useEffect, useRef } from "react";

const icons = {
  java: (
    <svg width="28" height="28" viewBox="0 0 24 24" fill="#ED8B00"><path d="M8.56 2.75c4.37 6.03 6.02 9.42 8.03 17.72m-7.88-1.86c10.94 2.27 12.94 5.46 13.82 7.77l-1.83.15M13.07 1c-1.83 8.97-2.6 13.39-8.38 16.3" stroke="#ED8B00" strokeWidth="1.5" fill="none" strokeLinecap="round"/></svg>
  ),
  js: (
    <svg width="28" height="28" viewBox="0 0 24 24"><rect width="24" height="24" rx="4" fill="#F7DF1E"/><text x="4" y="18" fontSize="14" fontWeight="bold" fill="#000">JS</text></svg>
  ),
  react: (
    <svg width="28" height="28" viewBox="0 0 24 24" fill="none"><circle cx="12" cy="12" r="2.5" fill="#61DAFB"/><ellipse cx="12" cy="12" rx="10" ry="4.5" stroke="#61DAFB" strokeWidth="1.5" fill="none"/><ellipse cx="12" cy="12" rx="10" ry="4.5" stroke="#61DAFB" strokeWidth="1.5" fill="none" transform="rotate(60 12 12)"/><ellipse cx="12" cy="12" rx="10" ry="4.5" stroke="#61DAFB" strokeWidth="1.5" fill="none" transform="rotate(120 12 12)"/></svg>
  ),
  node: (
    <svg width="28" height="28" viewBox="0 0 24 24"><path d="M12 2L2 7v10l10 5 10-5V7L12 2z" fill="#339933"/><text x="7" y="15" fontSize="8" fill="#fff" fontWeight="bold">Node</text></svg>
  ),
  spring: (
    <svg width="28" height="28" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10" fill="#6DB33F"/><path d="M8 16c0-4 4-4 4-8s4-4 4 0" stroke="#fff" strokeWidth="2" fill="none" strokeLinecap="round"/></svg>
  ),
  mongo: (
    <svg width="28" height="28" viewBox="0 0 24 24"><rect width="24" height="24" rx="4" fill="#47A248"/><path d="M12 4c-1 3-3 5-5 7s-2 5 0 8c1 2 3 3 5 3s4-1 5-3c2-3 1-6 0-8s-4-4-5-7z" fill="#fff"/></svg>
  ),
  mysql: (
    <svg width="28" height="28" viewBox="0 0 24 24"><rect width="24" height="24" rx="4" fill="#4479A1"/><text x="3" y="16" fontSize="9" fill="#fff" fontWeight="bold">MySQL</text></svg>
  ),
  tailwind: (
    <svg width="28" height="28" viewBox="0 0 24 24"><rect width="24" height="24" rx="4" fill="#38B2AC"/><path d="M6 12c2-6 10-6 12 0" stroke="#fff" strokeWidth="2.5" fill="none" strokeLinecap="round"/><path d="M6 16c2-6 10-6 12 0" stroke="#fff" strokeWidth="2.5" fill="none" strokeLinecap="round" opacity="0.6"/></svg>
  ),
  figma: (
    <svg width="28" height="28" viewBox="0 0 24 24"><rect width="24" height="24" rx="4" fill="#F24E1E"/><circle cx="12" cy="12" r="4" fill="#fff"/></svg>
  ),
  photoshop: (
    <svg width="28" height="28" viewBox="0 0 24 24"><rect width="24" height="24" rx="4" fill="#31A8FF"/><text x="5" y="17" fontSize="11" fill="#fff" fontWeight="bold">Ps</text></svg>
  ),
  premiere: (
    <svg width="28" height="28" viewBox="0 0 24 24"><rect width="24" height="24" rx="4" fill="#9999FF"/><text x="5" y="17" fontSize="11" fill="#fff" fontWeight="bold">Pr</text></svg>
  ),
  aftereffects: (
    <svg width="28" height="28" viewBox="0 0 24 24"><rect width="24" height="24" rx="4" fill="#9999FF"/><text x="5" y="17" fontSize="11" fill="#fff" fontWeight="bold">Ae</text></svg>
  ),
  illustrator: (
    <svg width="28" height="28" viewBox="0 0 24 24"><rect width="24" height="24" rx="4" fill="#FF9A00"/><text x="6" y="17" fontSize="11" fill="#fff" fontWeight="bold">Ai</text></svg>
  ),
  adobeXD: (
    <svg width="28" height="28" viewBox="0 0 24 24"><rect width="24" height="24" rx="4" fill="#FF61F6"/><text x="4" y="17" fontSize="11" fill="#fff" fontWeight="bold">XD</text></svg>
  ),
};

function Particle({ style }) {
  return <div className="absolute rounded-full" style={style} />;
}

function FloatingOrb({ size, color, top, left, delay }) {
  return (
    <div
      className="absolute rounded-full blur-3xl opacity-20 pointer-events-none"
      style={{
        width: size, height: size, background: color,
        top, left, animationDelay: delay,
        animation: "floatOrb 8s ease-in-out infinite",
      }}
    />
  );
}

function TechBadge({ icon, label, color }) {
  const [hovered, setHovered] = useState(false);
  return (
    <div
      onMouseEnter={() => setHovered(true)}
      onMouseLeave={() => setHovered(false)}
      className="relative cursor-pointer transition-all duration-300"
      style={{
        transform: hovered ? "translateY(-4px) scale(1.05)" : "translateY(0) scale(1)",
      }}
    >
      <div
        className="flex items-center gap-2 px-4 py-2 rounded-xl border transition-all duration-300"
        style={{
          background: hovered ? `${color}18` : "rgba(255,255,255,0.04)",
          borderColor: hovered ? color : "rgba(255,255,255,0.1)",
          boxShadow: hovered ? `0 0 20px ${color}40, 0 4px 20px rgba(0,0,0,0.3)` : "0 2px 10px rgba(0,0,0,0.2)",
        }}
      >
        <span style={{ filter: hovered ? `drop-shadow(0 0 8px ${color}80)` : "none", transition: "filter 0.3s" }}>
          {icon}
        </span>
        <span className="text-sm font-semibold" style={{ color: hovered ? "#fff" : "#a8b2d1", transition: "color 0.3s" }}>
          {label}
        </span>
      </div>
    </div>
  );
}

function StatCard({ title, value, icon, color }) {
  const [count, setCount] = useState(0);
  const ref = useRef(null);
  const target = parseInt(value) || 0;
  useEffect(() => {
    let start = 0;
    const step = Math.ceil(target / 40);
    const interval = setInterval(() => {
      start += step;
      if (start >= target) { setCount(target); clearInterval(interval); }
      else setCount(start);
    }, 30);
    return () => clearInterval(interval);
  }, [target]);

  return (
    <div className="relative overflow-hidden rounded-2xl border transition-all duration-300 hover:-translate-y-1"
      style={{
        background: "linear-gradient(135deg, rgba(255,255,255,0.06) 0%, rgba(255,255,255,0.02) 100%)",
        borderColor: "rgba(255,255,255,0.08)",
        boxShadow: "0 8px 32px rgba(0,0,0,0.3), inset 0 1px 0 rgba(255,255,255,0.08)",
      }}
    >
      <div className="absolute top-0 left-0 right-0 h-0.5" style={{ background: `linear-gradient(90deg, transparent, ${color}, transparent)` }} />
      <div className="p-5 text-center">
        <div className="text-2xl mb-1">{icon}</div>
        <div className="text-3xl font-bold" style={{ color, textShadow: `0 0 20px ${color}50` }}>
          {isNaN(target) ? value : count}
        </div>
        <div className="text-xs mt-1" style={{ color: "#64748b" }}>{title}</div>
      </div>
    </div>
  );
}

function SectionTitle({ children, icon }) {
  return (
    <div className="flex items-center gap-3 mb-6">
      <span className="text-2xl">{icon}</span>
      <h2 className="text-xl font-bold text-white relative">
        {children}
        <span className="absolute -bottom-1 left-0 w-full h-0.5 rounded-full" style={{ background: "linear-gradient(90deg, #6366f1, #a855f7, transparent)" }} />
      </h2>
    </div>
  );
}

function CodeBlock({ code, language = "typescript" }) {
  const lines = code.trim().split("\n");
  const keywords = ["const", "let", "var", "function", "return", "class", "import", "from", "export", "def", "self", "print", "if", "else"];
  const strings = /"[^"]*"|'[^']*'|`[^`]*`/g;
  const comments = /\/\/.*|#.*/g;

  const highlightLine = (line) => {
    const parts = [];
    let remaining = line;
    let key = 0;
    while (remaining.length > 0) {
      let earliest = null, earliestIdx = Infinity, type = null;
      const commentMatch = remaining.match(comments);
      if (commentMatch) {
        const idx = remaining.indexOf(commentMatch[0]);
        if (idx < earliestIdx) { earliest = commentMatch[0]; earliestIdx = idx; type = "comment"; }
      }
      const strMatch = remaining.match(strings);
      if (strMatch) {
        const idx = remaining.indexOf(strMatch[0]);
        if (idx < earliestIdx) { earliest = strMatch[0]; earliestIdx = idx; type = "string"; }
      }
      if (earliest === null) {
        const words = remaining.split(/(\s+|[{}()\[\]:,;=+\-*/<>!&|.])/);
        words.forEach(w => {
          if (keywords.includes(w.trim())) parts.push(<span key={key++} style={{ color: "#c792ea" }}>{w}</span>);
          else if (/^\d+$/.test(w.trim())) parts.push(<span key={key++} style={{ color: "#f78c6c" }}>{w}</span>);
          else parts.push(<span key={key++} style={{ color: "#a8b2d1" }}>{w}</span>);
        });
        break;
      }
      if (earliestIdx > 0) {
        const before = remaining.slice(0, earliestIdx);
        const words = before.split(/(\s+|[{}()\[\]:,;=+\-*/<>!&|.])/);
        words.forEach(w => {
          if (keywords.includes(w.trim())) parts.push(<span key={key++} style={{ color: "#c792ea" }}>{w}</span>);
          else if (/^\d+$/.test(w.trim())) parts.push(<span key={key++} style={{ color: "#f78c6c" }}>{w}</span>);
          else parts.push(<span key={key++} style={{ color: "#a8b2d1" }}>{w}</span>);
        });
      }
      if (type === "comment") parts.push(<span key={key++} style={{ color: "#546e7a", fontStyle: "italic" }}>{earliest}</span>);
      else if (type === "string") parts.push(<span key={key++} style={{ color: "#c3e88d" }}>{earliest}</span>);
      remaining = remaining.slice(earliestIdx + earliest.length);
    }
    return parts;
  };

  return (
    <div className="rounded-2xl overflow-hidden border" style={{ borderColor: "rgba(255,255,255,0.08)", background: "rgba(13,17,23,0.8)", boxShadow: "inset 0 1px 0 rgba(255,255,255,0.05)" }}>
      <div className="flex items-center gap-1.5 px-4 py-2.5" style={{ background: "rgba(255,255,255,0.03)", borderBottom: "1px solid rgba(255,255,255,0.06)" }}>
        <div className="w-3 h-3 rounded-full" style={{ background: "#ff5f57" }} />
        <div className="w-3 h-3 rounded-full" style={{ background: "#ffbd2e" }} />
        <div className="w-3 h-3 rounded-full" style={{ background: "#28c840" }} />
        <span className="ml-3 text-xs" style={{ color: "#546e7a" }}>{language}</span>
      </div>
      <div className="p-4 overflow-x-auto">
        <pre className="text-sm leading-relaxed" style={{ fontFamily: "'JetBrains Mono', 'Fira Code', monospace" }}>
          {lines.map((line, i) => (
            <div key={i} className="flex">
              <span className="inline-block w-8 text-right mr-4 select-none" style={{ color: "#3a4a5a", fontSize: "12px" }}>{i + 1}</span>
              <span>{highlightLine(line)}</span>
            </div>
          ))}
        </pre>
      </div>
    </div>
  );
}

function PillarCard({ icon, title, items, color, delay }) {
  const [visible, setVisible] = useState(false);
  useEffect(() => { const t = setTimeout(() => setVisible(true), delay); return () => clearTimeout(t); }, [delay]);
  return (
    <div className="rounded-2xl border p-5 transition-all duration-500 hover:-translate-y-1 hover:scale-[1.02]"
      style={{
        opacity: visible ? 1 : 0,
        transform: visible ? "translateY(0)" : "translateY(30px)",
        transition: "all 0.6s cubic-bezier(0.34,1.56,0.64,1)",
        background: "linear-gradient(145deg, rgba(255,255,255,0.06) 0%, rgba(255,255,255,0.02) 100%)",
        borderColor: "rgba(255,255,255,0.08)",
        boxShadow: "0 8px 32px rgba(0,0,0,0.3)",
      }}
    >
      <div className="flex items-center gap-2 mb-4">
        <span className="text-2xl">{icon}</span>
        <h3 className="font-bold text-lg" style={{ color }}>{title}</h3>
      </div>
      <div className="flex flex-wrap gap-2">
        {items.map((item, i) => (
          <span key={i} className="px-3 py-1 rounded-full text-xs font-medium" style={{ background: `${color}15`, color: color, border: `1px solid ${color}30` }}>
            {item}
          </span>
        ))}
      </div>
    </div>
  );
}

function CollabItem({ emoji, text, delay }) {
  const [visible, setVisible] = useState(false);
  useEffect(() => { const t = setTimeout(() => setVisible(true), delay); return () => clearTimeout(t); }, [delay]);
  return (
    <div className="flex items-start gap-3 group cursor-pointer" style={{ opacity: visible ? 1 : 0, transform: visible ? "translateX(0)" : "translateX(-40px)", transition: "all 0.5s cubic-bezier(0.34,1.56,0.64,1)" }}>
      <span className="text-xl mt-0.5 group-hover:scale-125 transition-transform duration-300">{emoji}</span>
      <span className="text-sm text-gray-300 group-hover:text-white transition-colors duration-300" style={{ borderLeft: "2px solid #6366f1", paddingLeft: "12px" }}>{text}</span>
    </div>
  );
}

function SocialLink({ icon, label, href, color }) {
  const [hovered, setHovered] = useState(false);
  return (
    <a href={href} target="_blank" rel="noreferrer"
      onMouseEnter={() => setHovered(true)}
      onMouseLeave={() => setHovered(false)}
      className="flex items-center gap-2.5 px-4 py-2.5 rounded-xl border transition-all duration-300 no-underline"
      style={{
        background: hovered ? `${color}12` : "rgba(255,255,255,0.04)",
        borderColor: hovered ? color : "rgba(255,255,255,0.1)",
        transform: hovered ? "scale(1.03)" : "scale(1)",
        boxShadow: hovered ? `0 0 20px ${color}30` : "none",
        textDecoration: "none",
      }}
    >
      <span className="text-lg">{icon}</span>
      <span className="text-sm font-semibold" style={{ color: hovered ? "#fff" : "#a8b2d1", transition: "color 0.3s" }}>{label}</span>
    </a>
  );
}

export default function App() {
  const [scrollY, setScrollY] = useState(0);
  const [mounted, setMounted] = useState(false);
  const containerRef = useRef(null);

  useEffect(() => {
    setMounted(true);
    const el = containerRef.current;
    if (el) {
      const handler = () => setScrollY(el.scrollTop);
      el.addEventListener("scroll", handler);
      return () => el.removeEventListener("scroll", handler);
    }
  }, []);

  const aboutCode = `const ashenShanilka = {
  name: "Ashen Shanilka Herath",
  username: "@Ashen365",
  location: "🇱🇰 Sri Lanka",
  education: "🎓 SLIIT – Faculty of Computing",

  roles: [
    "💻 Full Stack Developer",
    "🎨 UI/UX Designer (2+ Years)",
    "📸 Photographer & Videographer",
    "🎬 Content Creator"
  ],

  // Current goals & focus
  currentFocus: [
    "Building scalable web applications",
    "Creating stunning user experiences",
    "Learning advanced Java & Spring Boot"
  ],

  motto: "Stories into Software • Ideas into Animations",
  workMode: "☕ Coffee → 💡 Ideas → 💻 Code → 🚀 Deploy"
};`;

  const funCode = `class AshenShanilka:
    def __init__(self):
        self.pronouns = "He/Him"
        self.location = "Sri Lanka 🇱🇰"
        self.superpower = "Designing UI at 3AM"
        self.fuel = "☕ Coffee (lots of it)"
        self.philosophy = "Code is poetry"

    def daily_routine(self):
        # The sacred morning ritual
        return [
            "☕ Start with coffee",
            "💻 Write clean code",
            "🎨 Design beautiful UIs",
            "📸 Capture moments",
            "🚀 Deploy & iterate"
        ]

    def life_motto(self):
        return "Build the future, one pixel at a time"

# Initialize the legend
dev = AshenShanilka()
print(dev.life_motto())`;

  const devTechs = [
    { icon: icons.java, label: "Java", color: "#ED8B00" },
    { icon: icons.js, label: "JavaScript", color: "#F7DF1E" },
    { icon: icons.react, label: "React", color: "#61DAFB" },
    { icon: icons.node, label: "Node.js", color: "#339933" },
    { icon: icons.spring, label: "Spring Boot", color: "#6DB33F" },
    { icon: icons.mongo, label: "MongoDB", color: "#47A248" },
    { icon: icons.mysql, label: "MySQL", color: "#4479A1" },
    { icon: icons.tailwind, label: "Tailwind", color: "#38B2AC" },
  ];

  const designTechs = [
    { icon: icons.figma, label: "Figma", color: "#F24E1E" },
    { icon: icons.adobeXD, label: "Adobe XD", color: "#FF61F6" },
    { icon: icons.photoshop, label: "Photoshop", color: "#31A8FF" },
    { icon: icons.premiere, label: "Premiere", color: "#9999FF" },
    { icon: icons.aftereffects, label: "After Effects", color: "#9999FF" },
    { icon: icons.illustrator, label: "Illustrator", color: "#FF9A00" },
  ];

  const pillars = [
    { icon: "🎨", title: "Design", color: "#f472b6", items: ["UI/UX Design", "Motion Graphics", "Prototyping", "Brand Identity", "Wireframing"] },
    { icon: "💻", title: "Development", color: "#60a5fa", items: ["Full Stack Web", "MERN Stack", "Spring Boot APIs", "React + Tailwind", "Database Design"] },
    { icon: "🎬", title: "Content", color: "#a78bfa", items: ["Short Films", "Photography", "Videography", "Video Editing", "Social Media"] },
  ];

  const collabs = [
    { emoji: "🌐", text: "Open-source projects with stunning UI/UX" },
    { emoji: "📚", text: "Educational & skill-sharing platforms" },
    { emoji: "📱", text: "Innovative mobile and web applications" },
    { emoji: "🚀", text: "Creative tech solutions that make a difference" },
    { emoji: "🎨", text: "Design systems and component libraries" },
    { emoji: "🎬", text: "Tech + Creative content collaborations" },
  ];

  const socials = [
    { icon: "📧", label: "ashen365@gmail.com", href: "mailto:ashen365@gmail.com", color: "#D14836" },
    { icon: "💼", label: "LinkedIn", href: "https://www.linkedin.com/in/ashen-herath-b88879257/", color: "#0077B5" },
    { icon: "📱", label: "Instagram", href: "https://www.instagram.com/ashen_shanilka_herath/", color: "#E4405F" },
    { icon: "🎥", label: "YouTube", href: "https://www.youtube.com/@MonkeyMusichub", color: "#FF0000" },
  ];

  return (
    <>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap');
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { background: #0a0e1a; font-family: 'Inter', sans-serif; }
        @keyframes floatOrb {
          0%, 100% { transform: translate(0, 0) scale(1); }
          33% { transform: translate(30px, -40px) scale(1.1); }
          66% { transform: translate(-20px, 20px) scale(0.95); }
        }
        @keyframes heroIn {
          from { opacity: 0; transform: translateY(-30px); }
          to { opacity: 1; transform: translateY(0); }
        }
        @keyframes pulseGlow {
          0%, 100% { box-shadow: 0 0 20px rgba(99,102,241,0.3); }
          50% { box-shadow: 0 0 40px rgba(99,102,241,0.6), 0 0 60px rgba(168,85,247,0.2); }
        }
        @keyframes shimmer {
          0% { background-position: -200% center; }
          100% { background-position: 200% center; }
        }
        @keyframes spin-slow { to { transform: rotate(360deg); } }
        @keyframes bounce-subtle {
          0%, 100% { transform: translateY(0); }
          50% { transform: translateY(-4px); }
        }
        .glow-text {
          background: linear-gradient(135deg, #6366f1, #a855f7, #ec4899, #6366f1);
          background-size: 200% auto;
          -webkit-background-clip: text;
          -webkit-text-fill-color: transparent;
          background-clip: text;
          animation: shimmer 4s linear infinite;
        }
        .section-fade {
          opacity: 0;
          transform: translateY(20px);
          animation: heroIn 0.6s ease forwards;
        }
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: rgba(99,102,241,0.3); border-radius: 3px; }
        ::-webkit-scrollbar-thumb:hover { background: rgba(99,102,241,0.6); }
      `}</style>

      <div ref={containerRef} style={{ background: "#0a0e1a", minHeight: "100vh", overflowY: "auto", maxHeight: "100vh", color: "#e2e8f0", fontFamily: "'Inter', sans-serif", position: "relative" }}>

        {/* Ambient floating orbs */}
        <FloatingOrb size="400px" color="#6366f1" top="-100px" left="-100px" delay="0s" />
        <FloatingOrb size="300px" color="#a855f7" top="20%" left="75%" delay="2s" />
        <FloatingOrb size="250px" color="#ec4899" top="60%" left="10%" delay="4s" />
        <FloatingOrb size="200px" color="#6366f1" top="80%" left="60%" delay="1s" />

        <div className="relative z-10" style={{ maxWidth: "820px", margin: "0 auto", padding: "40px 24px 80px" }}>

          {/* ─── HERO ─── */}
          <div className="text-center" style={{ animation: "heroIn 0.8s cubic-bezier(0.34,1.56,0.64,1) forwards", opacity: 0 }}>
            {/* Avatar circle */}
            <div className="mx-auto mb-5 relative" style={{ width: "120px", height: "120px" }}>
              <div className="absolute inset-0 rounded-full" style={{ background: "linear-gradient(135deg, #6366f1, #a855f7, #ec4899)", animation: "spin-slow 4s linear infinite", padding: "3px" }}>
                <div className="w-full h-full rounded-full" style={{ background: "#0a0e1a" }} />
              </div>
              <div className="absolute inset-1.5 rounded-full flex items-center justify-center" style={{ background: "linear-gradient(135deg, #1e1b4b, #1e293b)" }}>
                <span style={{ fontSize: "48px" }}>👨‍💻</span>
              </div>
            </div>

            <h1 className="text-4xl font-extrabold mb-1" style={{ letterSpacing: "-0.02em" }}>
              <span className="glow-text">Ashen Shanilka Herath</span>
            </h1>
            <p className="text-sm mb-4" style={{ color: "#64748b" }}>@Ashen365 &nbsp;•&nbsp; 🇱🇰 Sri Lanka &nbsp;•&nbsp; 🎓 SLIIT</p>

            {/* Tagline with animated border */}
            <div className="inline-block mx-auto px-6 py-2.5 rounded-2xl border" style={{
              background: "rgba(99,102,241,0.06)",
              borderColor: "rgba(99,102,241,0.25)",
              animation: "pulseGlow 3s ease-in-out infinite",
            }}>
              <span className="text-sm font-semibold" style={{ color: "#a5b4fc" }}>
                ✨ Crafting Digital Experiences & Visual Stories ✨
              </span>
            </div>

            {/* Role pills */}
            <div className="flex flex-wrap justify-center gap-2 mt-4">
              {["💻 Full Stack Dev", "🎨 UI/UX Designer", "📸 Photographer", "🎬 Content Creator"].map((r, i) => (
                <span key={i} className="px-3 py-1 rounded-full text-xs font-medium" style={{
                  background: "rgba(255,255,255,0.05)",
                  border: "1px solid rgba(255,255,255,0.1)",
                  color: "#cbd5e1",
                  animation: `heroIn 0.5s ease ${0.15 * i + 0.3}s both`,
                }}>{r}</span>
              ))}
            </div>

            {/* Social badges */}
            <div className="flex flex-wrap justify-center gap-2 mt-5">
              {socials.map((s, i) => (
                <a key={i} href={s.href} target="_blank" rel="noreferrer" className="px-3 py-1.5 rounded-lg text-xs font-semibold no-underline transition-all duration-200"
                  style={{ background: `${s.color}18`, border: `1px solid ${s.color}40`, color: s.color, textDecoration: "none" }}
                  onMouseEnter={e => { e.currentTarget.style.background = `${s.color}30`; e.currentTarget.style.transform = "scale(1.08)"; }}
                  onMouseLeave={e => { e.currentTarget.style.background = `${s.color}18`; e.currentTarget.style.transform = "scale(1)"; }}
                >
                  {s.icon} {s.label}
                </a>
              ))}
            </div>

            {/* Profile views badge */}
            <div className="mt-4">
              <span className="inline-flex items-center gap-1.5 px-3 py-1 rounded-full text-xs" style={{ background: "rgba(99,102,241,0.12)", border: "1px solid rgba(99,102,241,0.25)", color: "#a5b4fc" }}>
                👁️ Profile Views &nbsp; <strong>2.4k+</strong>
              </span>
            </div>
          </div>

          {/* Divider */}
          <div className="my-10" style={{ height: "1px", background: "linear-gradient(90deg, transparent, rgba(99,102,241,0.4), rgba(168,85,247,0.4), transparent)" }} />

          {/* ─── ABOUT ME ─── */}
          <div className="mb-10" style={{ animation: "heroIn 0.6s ease 0.2s both", opacity: 0 }}>
            <SectionTitle icon="👨‍💻">About Me</SectionTitle>
            <CodeBlock code={aboutCode} language="typescript" />
          </div>

          {/* ─── STATS ROW ─── */}
          <div className="grid grid-cols-4 gap-3 mb-10" style={{ animation: "heroIn 0.6s ease 0.3s both", opacity: 0 }}>
            <StatCard title="Years Coding" value="3" icon="⚡" color="#6366f1" />
            <StatCard title="UI/UX Projects" value="20" icon="🎨" color="#a855f7" />
            <StatCard title="GitHub Repos" value="15" icon="📦" color="#60a5fa" />
            <StatCard title="Commits" value="450" icon="🔥" color="#f472b6" />
          </div>

          {/* ─── TECH STACK ─── */}
          <div className="mb-10" style={{ animation: "heroIn 0.6s ease 0.35s both", opacity: 0 }}>
            <SectionTitle icon="🛠️">Tech Stack & Tools</SectionTitle>
            <div className="mb-3">
              <p className="text-xs font-semibold mb-2" style={{ color: "#60a5fa", textTransform: "uppercase", letterSpacing: "0.08em" }}>⚙️ Development</p>
              <div className="flex flex-wrap gap-2">{devTechs.map((t, i) => <TechBadge key={i} {...t} />)}</div>
            </div>
            <div className="mt-4">
              <p className="text-xs font-semibold mb-2" style={{ color: "#f472b6", textTransform: "uppercase", letterSpacing: "0.08em" }}>🎨 Design & Creative</p>
              <div className="flex flex-wrap gap-2">{designTechs.map((t, i) => <TechBadge key={i} {...t} />)}</div>
            </div>
          </div>

          {/* ─── WHAT I DO (3 Pillars) ─── */}
          <div className="mb-10">
            <SectionTitle icon="🎯">What I Do</SectionTitle>
            <div className="grid grid-cols-3 gap-4">
              {pillars.map((p, i) => <PillarCard key={i} {...p} delay={i * 150 + 100} />)}
            </div>
          </div>

          {/* ─── LEARNING JOURNEY ─── */}
          <div className="mb-10" style={{ animation: "heroIn 0.6s ease 0.45s both", opacity: 0 }}>
            <SectionTitle icon="🚀">Currently Exploring</SectionTitle>
            <div className="grid grid-cols-4 gap-3">
              {[
                { title: "Backend", color: "#60a5fa", items: ["Advanced Java", "Spring Boot", "REST APIs", "Microservices"] },
                { title: "Frontend", color: "#34d399", items: ["React.js", "Next.js", "Tailwind CSS"] },
                { title: "Core CS", color: "#fbbf24", items: ["OOP", "Design Patterns", "DSA"] },
                { title: "Database", color: "#f472b6", items: ["SQL", "MongoDB", "Optimization"] },
              ].map((cat, i) => (
                <div key={i} className="rounded-xl border p-4" style={{ background: "rgba(255,255,255,0.03)", borderColor: "rgba(255,255,255,0.07)" }}>
                  <p className="text-xs font-bold mb-2" style={{ color: cat.color }}>{cat.title}</p>
                  {cat.items.map((item, j) => (
                    <div key={j} className="flex items-center gap-1.5 py-0.5">
                      <div className="w-1.5 h-1.5 rounded-full" style={{ background: cat.color }} />
                      <span className="text-xs" style={{ color: "#94a3b8" }}>{item}</span>
                    </div>
                  ))}
                </div>
              ))}
            </div>
          </div>

          {/* ─── GITHUB STATS (Mock) ─── */}
          <div className="mb-10" style={{ animation: "heroIn 0.6s ease 0.5s both", opacity: 0 }}>
            <SectionTitle icon="📊">GitHub Stats</SectionTitle>
            <div className="grid grid-cols-2 gap-4">
              {[
                { title: "Stats Overview", items: [["Repositories", "15"], ["Stars", "42"], ["Followers", "89"], ["Following", "120"]] },
                { title: "Top Languages", items: [["Java", "38%"], ["JavaScript", "28%"], ["CSS", "14%"], ["Python", "12%"]] },
              ].map((card, ci) => (
                <div key={ci} className="rounded-2xl border p-5" style={{ background: "linear-gradient(135deg, rgba(255,255,255,0.05), rgba(255,255,255,0.02))", borderColor: "rgba(255,255,255,0.08)" }}>
                  <p className="text-sm font-semibold mb-3" style={{ color: "#a5b4fc" }}>{card.title}</p>
                  {card.items.map((item, i) => (
                    <div key={i} className="flex justify-between items-center py-1.5">
                      <span className="text-xs" style={{ color: "#94a3b8" }}>{item[0]}</span>
                      <div className="flex items-center gap-2">
                        <div className="w-20 h-1.5 rounded-full" style={{ background: "rgba(255,255,255,0.08)" }}>
                          <div className="h-full rounded-full" style={{ width: `${(parseInt(item[1]) / (ci === 0 ? 120 : 40)) * 100}%`, background: "linear-gradient(90deg, #6366f1, #a855f7)", minWidth: "8px" }} />
                        </div>
                        <span className="text-xs font-bold" style={{ color: "#e2e8f0", width: "30px", textAlign: "right" }}>{item[1]}</span>
                      </div>
                    </div>
                  ))}
                </div>
              ))}
            </div>

            {/* Streak bar */}
            <div className="mt-4 rounded-2xl border p-4 text-center" style={{ background: "linear-gradient(135deg, rgba(249,115,22,0.08), rgba(239,68,68,0.05))", borderColor: "rgba(249,115,22,0.2)" }}>
              <span className="text-sm font-bold" style={{ color: "#fb923c" }}>🔥 Current Streak: <span style={{ color: "#fff" }}>12 days</span></span>
              <span className="mx-3" style={{ color: "#475569" }}>|</span>
              <span className="text-sm font-bold" style={{ color: "#fb923c" }}>📅 Longest Streak: <span style={{ color: "#fff" }}>28 days</span></span>
            </div>
          </div>

          {/* ─── COLLABORATE ─── */}
          <div className="mb-10">
            <SectionTitle icon="💡">Open to Collaborate On</SectionTitle>
            <div className="rounded-2xl border p-6" style={{ background: "linear-gradient(135deg, rgba(99,102,241,0.06), rgba(168,85,247,0.04))", borderColor: "rgba(99,102,241,0.15)" }}>
              <div className="flex flex-col gap-3">
                {collabs.map((c, i) => <CollabItem key={i} {...c} delay={i * 100 + 200} />)}
              </div>
            </div>
          </div>

          {/* ─── FUN FACTS ─── */}
          <div className="mb-10" style={{ animation: "heroIn 0.6s ease 0.55s both", opacity: 0 }}>
            <SectionTitle icon="⚡">Fun Facts</SectionTitle>
            <CodeBlock code={funCode} language="python" />
          </div>

          {/* ─── QUOTE ─── */}
          <div className="mb-10 text-center">
            <div className="inline-block px-8 py-5 rounded-2xl border" style={{ background: "linear-gradient(135deg, rgba(99,102,241,0.06), rgba(168,85,247,0.04))", borderColor: "rgba(99,102,241,0.15)" }}>
              <p className="text-lg font-semibold italic" style={{ color: "#c4b5fd" }}>
                "Code is poetry, Design is art — <span style={{ color: "#a78bfa" }}>and together they build the future.</span>"
              </p>
              <p className="text-xs mt-2" style={{ color: "#64748b" }}>— Ashen Shanilka Herath</p>
            </div>
          </div>

          {/* ─── FOOTER CTA ─── */}
          <div className="text-center rounded-3xl border p-8 relative overflow-hidden" style={{
            background: "linear-gradient(135deg, rgba(99,102,241,0.1), rgba(168,85,247,0.06), rgba(236,72,153,0.06))",
            borderColor: "rgba(99,102,241,0.2)",
            boxShadow: "0 0 60px rgba(99,102,241,0.15)",
          }}>
            <div className="absolute top-0 left-0 right-0 h-0.5" style={{ background: "linear-gradient(90deg, transparent, #6366f1, #a855f7, #ec4899, transparent)" }} />
            <h2 className="text-2xl font-bold text-white mb-2">🤝 Let's Connect & Create Together!</h2>
            <p className="text-sm mb-5" style={{ color: "#94a3b8" }}>
              💼 Open to freelance &nbsp;•&nbsp; 🤝 Available for collaborations &nbsp;•&nbsp; 📫 Always happy to connect!
            </p>
            <div className="flex flex-wrap justify-center gap-2">
              {socials.map((s, i) => <SocialLink key={i} {...s} />)}
            </div>
          </div>

          {/* ─── FOOTER ─── */}
          <div className="text-center mt-10 pb-4">
            <div className="inline-flex items-center gap-2 px-4 py-2 rounded-full" style={{ background: "rgba(99,102,241,0.08)", border: "1px solid rgba(99,102,241,0.15)" }}>
              <span className="text-sm" style={{ color: "#a5b4fc" }}>✨ Thanks for visiting!</span>
              <span className="text-sm" style={{ color: "#64748b" }}>|</span>
              <span className="text-sm" style={{ color: "#a5b4fc" }}>⭐ Star my repos!</span>
            </div>
            {/* wave footer */}
            <div className="mt-6" style={{ height: "60px", background: "linear-gradient(180deg, transparent, rgba(99,102,241,0.05))", borderRadius: "50% 50% 0 0 / 100% 100% 0 0" }} />
          </div>
        </div>
      </div>
    </>
  );
}
