import { useEffect } from "react";
import { motion } from "framer-motion";
import { Mail, Linkedin, Github } from "lucide-react";

export default function App() {
  useEffect(() => {
    const handleLinkClick = (e) => {
      const target = e.target.closest("a");
      if (target && target.getAttribute("href")?.startsWith("#")) {
        e.preventDefault();
        const id = target.getAttribute("href").slice(1);
        const section = document.getElementById(id);
        if (section) {
          section.scrollIntoView({ behavior: "smooth" });
        }
      }
    };

    document.addEventListener("click", handleLinkClick);
    return () => document.removeEventListener("click", handleLinkClick);
  }, []);

  return (
    <div className="min-h-screen bg-white text-gray-900 font-sans">
      {/* Navbar */}
      <header className="bg-white shadow p-6 sticky top-0 z-50">
        <div className="max-w-7xl mx-auto flex justify-between items-center">
          <h1 className="text-2xl font-bold tracking-wide">Shahwaiz Warraich</h1>
          <nav className="space-x-6 text-lg">
            <a href="#intro" className="hover:text-blue-600 transition-colors">Intro</a>
            <a href="#work" className="hover:text-blue-600 transition-colors">Work</a>
            <a href="#reviews" className="hover:text-blue-600 transition-colors">Reviews</a>
            <a href="#services" className="hover:text-blue-600 transition-colors">Services</a>
            <a href="#contact" className="hover:text-blue-600 transition-colors">Contact</a>
          </nav>
        </div>
      </header>

      {/* Hero Section */}
      <section id="intro" className="relative h-screen flex items-center bg-gradient-to-br from-blue-50 via-white to-blue-100 overflow-hidden">
        <div className="max-w-7xl mx-auto px-6 grid md:grid-cols-2 gap-12 items-center">
          {/* Left Side - Text */}
          <div className="text-center md:text-left">
            <motion.h2
              initial={{ opacity: 0, y: 40 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ duration: 1 }}
              className="text-6xl md:text-7xl font-extrabold mb-6 tracking-tight"
            >
              Hi, I’m Shahwaiz
            </motion.h2>
            <motion.p
              initial={{ opacity: 0 }}
              animate={{ opacity: 1 }}
              transition={{ delay: 0.6, duration: 1 }}
              className="text-xl md:text-2xl text-gray-600 max-w-xl"
            >
              A passionate Designer & Developer crafting modern, clean & impactful designs.
            </motion.p>
            <motion.a
              href="#work"
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ delay: 1, duration: 0.8 }}
              className="mt-10 inline-block px-8 py-4 bg-blue-600 text-white rounded-full shadow-lg hover:bg-blue-700 transition"
            >
              View My Work
            </motion.a>
          </div>

          {/* Right Side - Image */}
          <motion.img
            src="/images/profile.jpg"  // 👉 put your photo in /public/images/profile.jpg
            alt="Shahwaiz"
            initial={{ opacity: 0, scale: 0.9 }}
            animate={{ opacity: 1, scale: 1 }}
            transition={{ delay: 0.5, duration: 1 }}
            className="rounded-full shadow-2xl w-80 mx-auto md:mx-0"
          />
        </div>
      </section>

      {/* Work Section */}
      <section id="work" className="py-24 bg-gray-50">
        <div className="max-w-7xl mx-auto px-6">
          <h3 className="text-4xl font-bold mb-16 text-center">My Work</h3>
          {[
            { title: "Thumbnails", folder: "thumbnails" },
            { title: "Logos", folder: "logos" },
            { title: "Banners", folder: "banners" },
            { title: "Cards", folder: "cards" },
            { title: "Flyers", folder: "flyers" },
            { title: "Web Designs", folder: "webdesigns" },
            { title: "Ads", folder: "ads" },
          ].map((item, idx) => (
            <div key={idx} className="mb-20">
              <motion.h4
                initial={{ opacity: 0, x: -30 }}
                whileInView={{ opacity: 1, x: 0 }}
                transition={{ duration: 0.7 }}
                viewport={{ once: true }}
                className="text-2xl font-semibold mb-8"
              >
                {item.title}
              </motion.h4>
              <div className="grid md:grid-cols-3 gap-10">
                {Array.from({ length: 3 }).map((_, i) => (
                  <motion.div
                    key={i}
                    initial={{ opacity: 0, y: 20 }}
                    whileInView={{ opacity: 1, y: 0 }}
                    transition={{ duration: 0.6, delay: i * 0.1 }}
                    viewport={{ once: true }}
                    className="rounded-2xl overflow-hidden shadow-lg hover:shadow-2xl transition transform hover:-translate-y-2"
                  >
                    <img
                      src={`/images/${item.folder}/${i + 1}.jpg`} // 👉 upload images in /public/images/{folder}/1.jpg etc
                      alt={`${item.title} sample ${i + 1}`}
                      className="w-full h-56 object-cover"
                    />
                  </motion.div>
                ))}
              </div>
            </div>
          ))}
        </div>
      </section>

      {/* Reviews */}
      <section id="reviews" className="py-24 bg-white">
        <div className="max-w-7xl mx-auto px-6 text-center">
          <h3 className="text-4xl font-bold mb-16">What Clients Say</h3>
          <div className="grid md:grid-cols-3 gap-10">
            {[
              { text: "Amazing work, exceeded expectations.", name: "Aisha Khan", img: "/images/clients/client1.jpg" },
              { text: "Delivered fast and professional designs.", name: "Ali Raza", img: "/images/clients/client2.jpg" },
              { text: "Highly recommend — creative and reliable.", name: "Sana Malik", img: "/images/clients/client3.jpg" },
            ].map((review, i) => (
              <motion.div
                key={i}
                initial={{ opacity: 0, scale: 0.9 }}
                whileInView={{ opacity: 1, scale: 1 }}
                transition={{ duration: 0.6, delay: i * 0.2 }}
                viewport={{ once: true }}
                className="bg-gray-50 rounded-2xl p-8 shadow hover:shadow-lg transition flex flex-col items-center"
              >
                <img
                  src={review.img}
                  alt={review.name}
                  className="w-20 h-20 rounded-full mb-4 object-cover shadow-md"
                />
                <p className="text-gray-600 italic mb-4">“{review.text}”</p>
                <h4 className="font-semibold">{review.name}</h4>
              </motion.div>
            ))}
          </div>
        </div>
      </section>
    </div>
  );
}
