import React, { useState, useEffect } from 'react';
import { motion } from 'framer-motion';

const MonthsaryCelebration = () => {
  const [mwaElements, setMwaElements] = useState<{ id: number; x: number; y: number }[]>([]);

  useEffect(() => {
    const interval = setInterval(() => {
      if (mwaElements.length < 30) {
        const newMwa = {
          id: Date.now(),
          x: Math.random() * 80 + 10,
          y: Math.random() * 80 + 10,
        };
        setMwaElements((prev) => [...prev, newMwa]);
      }
    }, 300);

    return () => clearInterval(interval);
  }, [mwaElements.length]);

  return (
    <div className="min-h-screen bg-gradient-to-b from-pink-100 to-red-100 flex flex-col items-center justify-center p-4 relative overflow-hidden">
      {/* Main greeting */}
      <motion.h1 
        className="text-4xl md:text-6xl font-bold text-center text-pink-600 mb-8 z-10"
        initial={{ scale: 0.5, opacity: 0 }}
        animate={{ scale: 1, opacity: 1 }}
        transition={{ duration: 1 }}
      >
        Happy 3rd Monthsary Bebi !
      </motion.h1>

      {/* Balloons container */}
      <div className="flex flex-col md:flex-row justify-center items-center gap-6 md:gap-12 mb-12 z-10">
        {/* I Balloon */}
        <motion.div
          className="relative"
          initial={{ y: 100, opacity: 0 }}
          animate={{ y: 0, opacity: 1 }}
          transition={{ duration: 1, delay: 0.2 }}
        >
          <div className="w-24 h-32 bg-red-400 rounded-full flex items-center justify-center shadow-lg">
            <span className="text-white text-2xl font-bold">I</span>
          </div>
          <div className="absolute bottom-0 left-1/2 transform -translate-x-1/2 w-1 h-16 bg-gray-300"></div>
        </motion.div>

        {/* Love Balloon */}
        <motion.div
          className="relative"
          initial={{ y: 100, opacity: 0 }}
          animate={{ y: 0, opacity: 1 }}
          transition={{ duration: 1, delay: 0.4 }}
        >
          <div className="w-32 h-40 bg-pink-400 rounded-full flex items-center justify-center shadow-lg">
            <span className="text-white text-xl font-bold">Love</span>
          </div>
          <div className="absolute bottom-0 left-1/2 transform -translate-x-1/2 w-1 h-20 bg-gray-300"></div>
        </motion.div>

        {/* You Balloon */}
        <motion.div
          className="relative"
          initial={{ y: 100, opacity: 0 }}
          animate={{ y: 0, opacity: 1 }}
          transition={{ duration: 1, delay: 0.6 }}
        >
          <div className="w-24 h-32 bg-red-500 rounded-full flex items-center justify-center shadow-lg">
            <span className="text-white text-2xl font-bold">You</span>
          </div>
          <div className="absolute bottom-0 left-1/2 transform -translate-x-1/2 w-1 h-16 bg-gray-300"></div>
        </motion.div>
      </div>

      {/* Floating "mwa" elements */}
      <div className="absolute inset-0 pointer-events-none">
        {mwaElements.map((mwa) => (
          <motion.div
            key={mwa.id}
            className="absolute text-pink-400 font-bold text-xl md:text-2xl"
            style={{ left: `${mwa.x}%`, top: `${mwa.y}%` }}
            initial={{ scale: 0, opacity: 0 }}
            animate={{ scale: [0, 1.2, 1], opacity: [0, 1, 0] }}
            transition={{ duration: 2 }}
            onAnimationComplete={() => {
              setMwaElements((prev) => prev.filter((item) => item.id !== mwa.id));
            }}
          >
            mwa
          </motion.div>
        ))}
      </div>
    </div>
  );
};

export default MonthsaryCelebration;
