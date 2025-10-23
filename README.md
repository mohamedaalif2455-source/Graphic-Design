// Graphic Design Portfolio — Single-file React component
// Usage instructions (top):
// 1) This is a React component styled with Tailwind CSS. Drop into a Create React App / Vite / Next.js project.
// 2) Make sure Tailwind is installed and configured. Replace placeholder images and links with your own.
// 3) Export default is the component. Filename suggestion: GraphicPortfolio.jsx

import React, { useState } from "react";
import { motion } from "framer-motion";

const projectsData = [
  {
    id: 1,
    title: "Brand Identity for Cafe Luna",
    subtitle: "Logo + Visual System",
    img: "https://via.placeholder.com/800x600.png?text=Cafe+Luna",
    tags: ["Logo", "Branding", "Packaging"],
    description:
      "Developed a minimalist identity and packaging system for a boutique cafe. Included logo, color palette, typography guidance and mockups.",
    github: "https://github.com/your-username/cafe-luna",
    live: "#"
  },
  {
    id: 2,
    title: "Event Poster Series",
    subtitle: "Poster Designs for Music Fest",
    img: "https://via.placeholder.com/800x600.png?text=Music+Fest",
    tags: ["Poster", "Illustration", "Print"],
    description:
      "A series of posters exploring bold typography and layered textures for a regional music festival.",
    github: "https://github.com/your-username/music-posters",
    live: "#"
  },
  {
    id: 3,
    title: "Social Media Campaign — BrightSkin",
    subtitle: "Ads + Carousel",
    img: "https://via.placeholder.com/800x600.png?text=BrightSkin",
    tags: ["Social", "Ads", "Motion"],
    description:
      "Concept, visuals, and motion-ready assets for a skincare brand's seasonal campaign.",
    github: "https://github.com/your-username/brightskin-campaign",
    live: "#"
  }
];

export default function GraphicPortfolio() {
  const [selected, setSelected] = useState(null);
  const [query, setQuery] = useState("");

  const filtered = projectsData.filter((p) => {
    const q = query.toLowerCase();
    return (
      p.title.toLowerCase().includes(q) ||
      p.tags.join(" ").toLowerCase().includes(q) ||
      p.subtitle.toLowerCase().includes(q)
    );
  });

  return (
    <div className="min-h-screen bg-gray-50 text-gray-900">
      <header className="max-w-6xl mx-auto px-6 py-10">
        <div className="flex items-center justify-between">
          <div>
            <h1 className="text-3xl font-extrabold">Mohamed Aalif — Graphic Designer</h1>
            <p className="mt-1 text-sm text-gray-600">Visual identity, posters, social campaigns, and packaging.</p>
          </div>
          <nav className="space-x-4 text-sm">
            <a href="#portfolio" className="hover:underline">Portfolio</a>
            <a href="#about" className="hover:underline">About</a>
            <a href="#contact" className="hover:underline">Contact</a>
          </nav>
        </div>
      </header>

      <main className="max-w-6xl mx-auto px-6 pb-20">
        {/* Hero */}
        <section className="grid md:grid-cols-2 gap-8 items-center mb-12">
          <div>
            <motion.h2
              initial={{ opacity: 0, y: 10 }}
              animate={{ opacity: 1, y: 0 }}
              transition={{ duration: 0.5 }}
              className="text-4xl font-bold leading-tight"
            >
              I craft bold, memorable visual experiences.
            </motion.h2>
            <p className="mt-4 text-gray-700">
              Hi—I’m a graphic designer focused on brand identity, poster series and social creatives. I combine strategy with handcrafted visuals to help brands stand out.
            </p>
            <div className="mt-6 flex gap-3">
              <a href="#portfolio" className="px-4 py-2 bg-black text-white rounded-lg text-sm">View Work</a>
              <a href="#contact" className="px-4 py-2 border border-gray-300 rounded-lg text-sm">Hire me</a>
            </div>
            <div className="mt-6 text-sm text-gray-500">Tip: Replace placeholder images with your exported PNG/JPEG or direct links to Behance/Dribbble.</div>
          </div>
          <div className="flex items-center justify-center">
            <div className="w-full max-w-md rounded-2xl overflow-hidden shadow-lg">
              <img src="https://via.placeholder.com/800x600.png?text=Featured+Work" alt="featured" className="w-full object-cover" />
            </div>
          </div>
        </section>

        {/* Search + filters */}
        <section className="mb-8">
          <input
            value={query}
            onChange={(e) => setQuery(e.target.value)}
            placeholder="Search projects or tags (e.g., Logo, Poster)"
            className="w-full max-w-lg px-4 py-3 rounded-lg border border-gray-200 shadow-sm"
          />
        </section>

        {/* Portfolio Grid */}
        <section id="portfolio">
          <h3 className="text-2xl font-semibold mb-4">Selected Projects</h3>
          <div className="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">
            {filtered.map((p) => (
              <motion.article
                key={p.id}
                whileHover={{ scale: 1.02 }}
                className="bg-white rounded-2xl overflow-hidden shadow"
              >
                <button className="text-left w-full" onClick={() => setSelected(p)}>
                  <div className="h-44 overflow-hidden">
                    <img src={p.img} alt={p.title} className="w-full h-full object-cover" />
                  </div>

                  <div className="p-4">
                    <h4 className="font-semibold">{p.title}</h4>
                    <p className="mt-1 text-sm text-gray-500">{p.subtitle}</p>
                    <div className="mt-3 flex flex-wrap gap-2">
                      {p.tags.map((t) => (
                        <span key={t} className="text-xs px-2 py-1 rounded-full border border-gray-200">{t}</span>
                      ))}
                    </div>
                  </div>
                </button>
              </motion.article>
            ))}
          </div>
        </section>

        {/* Modal */}
        {selected && (
          <div className="fixed inset-0 z-40 flex items-center justify-center p-6">
            <div className="absolute inset-0 bg-black/40" onClick={() => setSelected(null)}></div>
            <motion.div
              initial={{ opacity: 0, scale: 0.95 }}
              animate={{ opacity: 1, scale: 1 }}
              className="relative z-50 max-w-3xl w-full bg-white rounded-2xl shadow-lg overflow-hidden"
            >
              <div className="p-4 flex justify-between items-start">
                <div>
                  <h4 className="text-xl font-bold">{selected.title}</h4>
                  <p className="text-sm text-gray-600">{selected.subtitle}</p>
                </div>
                <button onClick={() => setSelected(null)} className="text-gray-500">Close</button>
              </div>
              <div className="p-4">
                <img src={selected.img} alt={selected.title} className="w-full h-64 object-cover rounded-md" />
                <p className="mt-4 text-gray-700">{selected.description}</p>
                <div className="mt-4 flex gap-3">
                  <a href={selected.github} target="_blank" rel="noreferrer" className="px-3 py-2 border rounded-lg text-sm">View repo</a>
                  <a href={selected.live} target="_blank" rel="noreferrer" className="px-3 py-2 border rounded-lg text-sm">Live / Mockup</a>
                </div>
              </div>
            </motion.div>
          </div>
        )}

        {/* About + Contact */}
        <section id="about" className="mt-12 bg-white rounded-2xl p-6 shadow">
          <h3 className="text-xl font-semibold">About me</h3>
          <p className="mt-2 text-gray-700">I’m a graphic designer who loves solving brand problems with strong visuals. I work across identity, print and digital campaigns. I’m available for freelance and full-time work.</p>
          <div className="mt-4 grid sm:grid-cols-2 gap-4">
            <div>
              <p className="text-sm text-gray-600">Skills</p>
              <ul className="mt-2 list-disc list-inside text-gray-700">
                <li>Brand Identity</li>
                <li>Poster & Print Design</li>
                <li>Social Media Creatives</li>
                <li>Adobe Photoshop / Illustrator / InDesign</li>
              </ul>
            </div>
            <div>
              <p className="text-sm text-gray-600">Availability</p>
              <p className="mt-2 text-gray-700">Open to freelance projects. Available from Mon — Fri. Rates vary based on scope.</p>
            </div>
          </div>
        </section>

        <section id="contact" className="mt-8">
          <h3 className="text-xl font-semibold">Contact</h3>
          <div className="mt-3 grid sm:grid-cols-2 gap-6">
            <form className="space-y-3 bg-white rounded-2xl p-4 shadow">
              <input placeholder="Your name" className="w-full px-3 py-2 border rounded-md" />
              <input placeholder="Email" className="w-full px-3 py-2 border rounded-md" />
              <textarea placeholder="Message" className="w-full px-3 py-2 border rounded-md h-28" />
              <div className="flex justify-end">
                <button type="button" className="px-4 py-2 bg-black text-white rounded-lg">Send</button>
              </div>
            </form>

            <div className="p-4">
              <p className="text-sm text-gray-600">Other links</p>
              <ul className="mt-3 space-y-2">
                <li><a href="https://github.com/your-username" target="_blank" rel="noreferrer" className="underline">GitHub</a></li>
                <li><a href="#" target="_blank" rel="noreferrer" className="underline">Behance</a></li>
                <li><a href="#" target="_blank" rel="noreferrer" className="underline">Dribbble</a></li>
              </ul>
              <div className="mt-6 text-sm text-gray-500">Pro tip: Link the GitHub repos to zipped source files or a README that explains deliverables and export steps for clients.</div>
            </div>
          </div>
        </section>

        <footer className="mt-12 text-center text-sm text-gray-500">© {new Date().getFullYear()} Mohamed Aalif — Crafted with care.</footer>
      </main>
    </div>
  );
}
