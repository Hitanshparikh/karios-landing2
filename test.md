okay now see, i want to create one new page, that will be our hero page after logining in, the main page, that will work literally like voice assistant, that can do every single thing, either i can chat or i can use voice assistant, and it can do everytihngn, literally everything on this app, it can perform what our all 4 main functionalities that are finance, veto, nutrition(meal planning and other stuff, recon and memory keeping,) now this all things, every activity that user does, it gets saved in memory graph for future references, this ai should work the best, fastest responses and best ui, now i will share you eleven labs api key: sk_c45345d901de8c7e57b33cac8aada1f0a648adb1a1d89bd7

and you can you gemini api that i have already shared to compute all the ai stuff, our ai should be most intelligent, most powerfull, but at the same time fastest reponses, lowest latency and best accurate replies adn actions, should be understanding and should make user's life and experience easy, 

now here is the component that you should use:
use this for ai chat component:
'use client';

import React, { useState, useRef, useEffect } from 'react';
import { motion, AnimatePresence } from 'motion/react';
import { ArrowUp, Youtube } from 'lucide-react';

export type MentionType = 'google' | 'youtube' | null;

export interface MessageReply01 {
  id: string;
  text: string;
  sender: 'user' | 'ai';
  mention?: MentionType;
  timestamp: number;
}

interface AiInput003Props {
  onSendMessage?: (message: string, mention: MentionType) => void;
  placeholder?: string;
}

const MentionBadge: React.FC<{ type: MentionType; compact?: boolean }> = ({
  type,
  compact = false,
}) => {
  if (!type) return null;
  const isGoogle = type === 'google';
  const label = isGoogle ? 'Google Search' : 'Youtube Analyzer';

  return (
    <div
      className={`flex items-center gap-2 rounded-xl px-3 py-1.5 transition-all duration-300 select-none ${compact ? 'text-xs' : 'text-sm'} border border-neutral-200 bg-neutral-100 dark:border-[#333] dark:bg-[#222]`}
    >
      {isGoogle ? (
        <div className="flex h-5 w-5 items-center justify-center rounded-md border border-neutral-100 bg-white shadow-sm dark:border-transparent">
          <svg viewBox="0 0 24 24" width="14" height="14">
            <path
              d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"
              fill="#4285F4"
            />
            <path
              d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"
              fill="#34A853"
            />
            <path
              d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.07H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.93l3.66-2.84z"
              fill="#FBBC05"
            />
            <path
              d="M12 5.38c1.62 0 3.06.56 4.21 1.66l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.07l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"
              fill="#EA4335"
            />
          </svg>
        </div>
      ) : (
        <div className="flex h-5 w-5 items-center justify-center rounded-md bg-red-600 shadow-sm">
          <Youtube size={14} className="fill-white text-white" />
        </div>
      )}
      <span className="font-medium text-neutral-600 dark:text-neutral-300">
        {label}
      </span>
    </div>
  );
};

export const AiInput003: React.FC<AiInput003Props> = ({
  onSendMessage,
  placeholder = 'Type shit..',
}) => {
  const [inputValue, setInputValue] = useState('');
  const [messages, setMessages] = useState<MessageReply01[]>([]);
  const [isTyping, setIsTyping] = useState(false);
  const [isSending, setIsSending] = useState(false);
  const [mention, setMention] = useState<MentionType>(null);
  const scrollRef = useRef<HTMLDivElement>(null);

  useEffect(() => {
    if (scrollRef.current) {
      scrollRef.current.scrollTo({
        top: scrollRef.current.scrollHeight,
        behavior: 'smooth',
      });
    }
  }, [messages, isTyping]);

  const handleInputChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    const val = e.target.value;
    setInputValue(val);
    if (val.includes('@goog')) setMention('google');
    else if (val.includes('@yt')) setMention('youtube');
    else if (!val.includes('@')) setMention(null);
  };

  const handleSendMessage = async () => {
    if (!inputValue.trim() || isSending) return;

    setIsSending(true);
    const userMessage: MessageReply01 = {
      id: Date.now().toString(),
      text: inputValue,
      sender: 'user',
      mention: mention,
      timestamp: Date.now(),
    };

    setMessages((prev) => [...prev, userMessage]);
    if (onSendMessage) onSendMessage(inputValue, mention);

    setInputValue('');
    setMention(null);

    setTimeout(() => {
      setIsSending(false);
      setIsTyping(true);

      setTimeout(() => {
        const aiMessage: MessageReply01 = {
          id: (Date.now() + 1).toString(),
          text: 'This is a simulated response.',
          sender: 'ai',
          timestamp: Date.now(),
        };
        setMessages((prev) => [...prev, aiMessage]);
        setIsTyping(false);
      }, 1500);
    }, 400);
  };

  return (
    <div className="relative flex h-screen w-full flex-col overflow-hidden border-x border-neutral-200 bg-white text-neutral-900 selection:bg-neutral-200 dark:border-neutral-800/50 dark:bg-black dark:text-white dark:selection:bg-white/20">
      <div className="pointer-events-none absolute inset-0">
        <div className="absolute -bottom-[10%] left-1/2 h-[30%] w-[100%] -translate-x-1/2 bg-neutral-100/50 blur-[120px] dark:bg-neutral-500/10" />
      </div>

      <div
        ref={scrollRef}
        className="custom-scrollbar relative z-10 flex flex-1 flex-col overflow-y-auto px-4"
      >
        <div className="flex-grow" />
        <div className="mx-auto w-full max-w-2xl space-y-6 py-10">
          <AnimatePresence initial={false}>
            {messages.map((msg) => (
              <motion.div
                key={msg.id}
                initial={{ opacity: 0, scale: 0.95, y: 10 }}
                animate={{ opacity: 1, scale: 1, y: 0 }}
                className={`flex flex-col ${msg.sender === 'user' ? 'items-end' : 'items-start'}`}
              >
                <div
                  className={`max-w-[85%] rounded-[10px] px-5 py-3 text-[15px] leading-relaxed shadow-sm transition-colors duration-300 ${
                    msg.sender === 'user'
                      ? 'rounded-br-none border border-neutral-200 bg-neutral-100 text-neutral-800 dark:border-neutral-800/50 dark:bg-[#1a1a1a] dark:text-neutral-100'
                      : 'border border-neutral-100 bg-neutral-50 text-neutral-700 dark:border-neutral-800/30 dark:bg-neutral-900/40 dark:text-neutral-200'
                  }`}
                >
                  {msg.text}
                </div>

                {msg.mention && msg.sender === 'user' && (
                  <div className="mt-2">
                    <MentionBadge type={msg.mention} compact />
                  </div>
                )}
              </motion.div>
            ))}
          </AnimatePresence>

          {isTyping && (
            <div className="flex h-6 items-center gap-1.5 px-4">
              <div className="h-1 w-1 animate-bounce rounded-full bg-neutral-300 [animation-delay:-0.3s] dark:bg-neutral-500" />
              <div className="h-1 w-1 animate-bounce rounded-full bg-neutral-300 [animation-delay:-0.15s] dark:bg-neutral-500" />
              <div className="h-1 w-1 animate-bounce rounded-full bg-neutral-300 dark:bg-neutral-500" />
            </div>
          )}
        </div>
      </div>

      <div className="relative z-20 flex w-full items-center justify-center  px-4 pt-4 pb-12 transition-colors duration-300 dark:from-black dark:via-black">
        <div className="relative w-full max-w-2xl">
          <AnimatePresence>
            {mention && (
              <motion.div
                initial={{ opacity: 0, y: 10, scale: 0.95 }}
                animate={{ opacity: 1, y: 0, scale: 1 }}
                exit={{ opacity: 0, y: 10, scale: 0.95 }}
                className="absolute bottom-full left-4 mb-4"
              >
                <MentionBadge type={mention} />
              </motion.div>
            )}
          </AnimatePresence>

          <motion.div
            animate={{
              scale: isSending ? 0.985 : 1,
              borderColor: isSending ? 'rgba(239,68,68,0.35)' : 'transparent',
              boxShadow: isSending
                ? '0 0 18px rgba(239,68,68,0.12)'
                : '0 4px 12px rgba(0,0,0,0.03)',
            }}
            transition={{
              type: 'spring',
              stiffness: 300,
              damping: 28,
            }}
            className="group relative flex items-center overflow-hidden rounded-full border border-neutral-700 bg-black/5 px-6 py-3 pr-4 transition-colors duration-300 dark:border-neutral-800 dark:bg-neutral-800/70 dark:shadow-sm"
          >
            {isSending && (
              <motion.div
                initial={{ y: '220%' }}
                animate={{ y: '-120%' }}
                transition={{
                  duration: 0.6,
                  ease: 'easeInOut',
                }}
                className="pointer-events-none absolute inset-0 z-0 skew-x-12 bg-gradient-to-t from-red-500/25 via-red-500/10 to-white/10 blur-md"
              />
            )}

            <input
              type="text"
              value={inputValue}
              onChange={handleInputChange}
              onKeyDown={(e) => e.key === 'Enter' && handleSendMessage()}
              placeholder={placeholder}
              className="z-10 flex-1 border-none bg- py-2 text-[18px] font-semibold text-neutral-900 placeholder-neutral-400 outline-none dark:text-neutral-100 dark:placeholder-neutral-500"
              autoFocus
            />

            <motion.button
              whileTap={{ scale: 0.9 }}
              onClick={handleSendMessage}
              disabled={!inputValue.trim()}
              className={`z-10 ml-4 flex h-10 w-10 items-center justify-center rounded-full transition-all duration-300 ${
                inputValue.trim()
                  ? 'bg-neutral-900 text-white shadow-sm shadow-neutral-200 active:scale-95 dark:bg-white dark:text-black dark:shadow-none'
                  : 'bg-neutral-50 text-neutral-400  dark:bg-neutral-700 dark:text-neutral-200'
              }`}
            >
              <ArrowUp size={20} strokeWidth={3} />
            </motion.button>
          </motion.div>
        </div>
      </div>
    </div>
  );
};


and i will share you small 3d modeled cute robot that will be acting like our assistant and will do gestures by moving to comunicate more better and more interesting way instead of just staying idle, now it can't move its legs or hands or its body or its face or and it has no expressions too, so you need to do something smart and hovering over it bring its attention, so you need to animate it to make it more interesting to work, it should make humans talk to it more freely and in easy way, that it understands, and if possible, it can understand multi language like hindi gujarati, english, or maybe mix, but it should be accurate and fast, adn in small texts like captions we can show what is transcribed and what our ai speaks, the captions are shown too, properly, and the model should be in proper size so its not too small and not too big too, just perfectly set and some effects added to make it look cool and premium, it should be interactive and should be interesting, here is its model in .glb format:
baymax\baymax_operacao_big_hero.glb

use stich to generate best design for it, i want best ai agent and best ui for this specific page, that will be our main functionality for everything, it should be able to generate stuff, it should be able to do literally everytihng, normal ai works already, over that it would have context of all my memory, my preferences and my activities on this app, and also my all the datas and my moods adn my financial datas and everything, so that it can do anything for me, literally i will talk to it naturally how i would talk to my friend or buddy and it will do the tasks and save the memories and everything, it can be my talk buddy too, and something interesting, something that will make us win this competition, it can help me plan my perfect nuttricios meal, help me make right decisions aleady knowning most of the contexts, help me with all the stuffs, it should be like my assitant, it can also take care of my health, as much as we can provide, it can help me schedule things, it can help me remind my tasks, it can help me give clarity when im confused, it should be friendly and realistic and less ai generative, so basically the 3d model that i shared was of baymax, that character that you can search online, it should be super intelligenet adn should do eveyritng that i mentioned above, take your time but i want it to be working by today itself, create a long detailed plan adn save it as file in our repo so that you can never forget the idea, the contexts and exactly whats in my mind, please keep it detailed, like i shared you, so that we don't loose any of it, and we can implement all of it

create a proper planning okay and tasks so we make it perfectly without any issues and errors, it should work well without any errors or issues and smoothly and fast reponses and almost very very lowest delays and quick answers if possible, and also save everything to databse to create user idenetity like our app already does, so it has all the references and knowledge of the user

use stich for best ui and ux and everything for this page and also make it mobile friendly and responsive and as minimall as possible like trillion dollar ai s and companies