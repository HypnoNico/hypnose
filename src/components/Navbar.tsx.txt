import { useState, useEffect } from "react";
import { motion } from "framer-motion";
import { Phone, Menu, X } from "lucide-react";

const Navbar = () => {
  const [scrolled, setScrolled] = useState(false);
  const [menuOpen, setMenuOpen] = useState(false);

  useEffect(() => {
    const onScroll = () => setScrolled(window.scrollY > 50);
    window.addEventListener("scroll", onScroll);
    return () => window.removeEventListener("scroll", onScroll);
  }, []);

  const links = [
    { label: "Prestations", href: "#prestations" },
    { label: "Contact", href: "#contact" },
  ];

  return (
    <motion.nav
      className={`fixed top-0 left-0 right-0 z-50 transition-all duration-500 ${
        scrolled
          ? "bg-background/80 backdrop-blur-xl border-b border-border/50"
          : "bg-transparent"
      }`}
      initial={{ y: -80 }}
      animate={{ y: 0 }}
      transition={{ duration: 0.6 }}
    >
      <div className="max-w-6xl mx-auto px-6 py-4 flex items-center justify-between">
        <a href="#" className="font-display text-2xl font-bold text-gradient-gold">
          HypnoNico
        </a>

        {/* Desktop */}
        <div className="hidden md:flex items-center gap-8">
          {links.map((l) => (
            <a
              key={l.href}
              href={l.href}
              className="text-muted-foreground hover:text-foreground transition-colors text-sm font-body tracking-wide"
            >
              {l.label}
            </a>
          ))}
          <a
            href="tel:+33756966024"
            className="flex items-center gap-2 px-5 py-2.5 bg-primary text-primary-foreground font-body font-semibold text-sm rounded-lg transition-all duration-300 hover:shadow-[0_0_30px_hsl(38_90%_55%/0.3)]"
          >
            <Phone className="w-4 h-4" />
            Réserver
          </a>
        </div>

        {/* Mobile toggle */}
        <button
          className="md:hidden text-foreground"
          onClick={() => setMenuOpen(!menuOpen)}
          aria-label="Menu"
        >
          {menuOpen ? <X className="w-6 h-6" /> : <Menu className="w-6 h-6" />}
        </button>
      </div>

      {/* Mobile menu */}
      {menuOpen && (
        <motion.div
          className="md:hidden bg-background/95 backdrop-blur-xl border-t border-border/50 px-6 pb-6 pt-4 flex flex-col gap-4"
          initial={{ opacity: 0, y: -10 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.2 }}
        >
          {links.map((l) => (
            <a
              key={l.href}
              href={l.href}
              onClick={() => setMenuOpen(false)}
              className="text-foreground font-body text-lg"
            >
              {l.label}
            </a>
          ))}
          <a
            href="tel:+33756966024"
            className="flex items-center gap-2 px-5 py-3 bg-primary text-primary-foreground font-body font-semibold rounded-lg justify-center"
          >
            <Phone className="w-4 h-4" />
            07 56 96 60 24
          </a>
        </motion.div>
      )}
    </motion.nav>
  );
};

export default Navbar;
