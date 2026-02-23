import { motion, useInView } from "framer-motion";
import { useRef } from "react";
import { Phone, Mail, MapPin } from "lucide-react";

const CTASection = () => {
  const ref = useRef(null);
  const isInView = useInView(ref, { once: true, margin: "-80px" });

  return (
    <section ref={ref} id="contact" className="section-padding relative overflow-hidden">
      {/* Glow effect behind */}
      <div className="absolute inset-0 flex items-center justify-center pointer-events-none">
        <div className="w-[600px] h-[600px] rounded-full bg-primary/5 blur-[120px]" />
      </div>

      <div className="relative z-10 max-w-4xl mx-auto">
        <motion.div
          className="glass-card p-10 md:p-16 text-center border-primary/15"
          initial={{ opacity: 0, scale: 0.95 }}
          animate={isInView ? { opacity: 1, scale: 1 } : {}}
          transition={{ duration: 0.8 }}
        >
          <p className="text-primary/70 font-body text-sm tracking-[0.3em] uppercase mb-4">
            Prêt à vivre l'expérience ?
          </p>
          <h2 className="text-3xl md:text-5xl font-display font-bold text-gradient-gold mb-6">
            Réservez Votre Spectacle
          </h2>
          <p className="text-muted-foreground text-lg max-w-xl mx-auto mb-10 leading-relaxed">
            Chaque événement mérite un moment d'exception. Contactez-moi pour
            créer ensemble un spectacle inoubliable.
          </p>

          <div className="flex flex-col sm:flex-row gap-4 justify-center items-center mb-10">
            <a
              href="tel:+33756966024"
              className="group flex items-center gap-3 px-8 py-4 bg-primary text-primary-foreground font-body font-semibold text-lg rounded-lg transition-all duration-300 hover:shadow-[0_0_40px_hsl(38_90%_55%/0.4)] animate-pulse-glow"
            >
              <Phone className="w-5 h-5" />
              07 56 96 60 24
            </a>
            <a
              href="mailto:contact@hypnonico.fr"
              className="flex items-center gap-3 px-8 py-4 glass-card border-primary/20 text-foreground font-body font-medium rounded-lg transition-all duration-300 hover:border-primary/40"
            >
              <Mail className="w-5 h-5 text-primary" />
              Me contacter
            </a>
          </div>

          <div className="flex items-center justify-center gap-2 text-muted-foreground text-sm">
            <MapPin className="w-4 h-4 text-primary/60" />
            <span>Disponible partout en France</span>
          </div>
        </motion.div>
      </div>
    </section>
  );
};

export default CTASection;
