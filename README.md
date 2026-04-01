import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";

const questions = [
  {
    q: "데이트에서 나는 어떤 편?",
    options: [
      { text: "계획적으로 준비한다", type: "A" },
      { text: "즉흥적으로 즐긴다", type: "B" },
    ],
  },
  {
    q: "연인과의 연락 스타일은?",
    options: [
      { text: "자주 연락", type: "A" },
      { text: "필요할 때만", type: "B" },
    ],
  },
  {
    q: "갈등이 생기면?",
    options: [
      { text: "대화를 통해 해결", type: "A" },
      { text: "시간을 갖는다", type: "B" },
    ],
  },
  {
    q: "이상적인 데이트는?",
    options: [
      { text: "조용한 카페", type: "A" },
      { text: "액티비티", type: "B" },
    ],
  },
  {
    q: "연애에서 중요한 것은?",
    options: [
      { text: "안정감", type: "A" },
      { text: "설렘", type: "B" },
    ],
  },
];

export default function App() {
  const [step, setStep] = useState(0);
  const [answers, setAnswers] = useState([]);

  const handleAnswer = (type) => {
    const newAnswers = [...answers, type];
    setAnswers(newAnswers);
    setStep(step + 1);
  };

  const getResult = () => {
    const countA = answers.filter((a) => a === "A").length;
    if (countA >= 3)
      return {
        title: "안정형 연애 스타일",
        desc: "신뢰와 안정감을 중요시하는 스타일",
        match: "자유로운 스타일과 잘 맞아요!",
      };
    return {
      title: "자유형 연애 스타일",
      desc: "설렘과 즐거움을 추구하는 스타일",
      match: "안정적인 스타일과 잘 맞아요!",
    };
  };

  return (
    <div className="flex items-center justify-center min-h-screen bg-gray-100 p-4">
      <Card className="w-full max-w-md rounded-2xl shadow-xl">
        <CardContent className="p-6">
          {step < questions.length ? (
            <motion.div
              key={step}
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
            >
              <h2 className="text-xl font-bold mb-4">
                {questions[step].q}
              </h2>
              <div className="space-y-2">
                {questions[step].options.map((opt, i) => (
                  <Button
                    key={i}
                    className="w-full"
                    onClick={() => handleAnswer(opt.type)}
                  >
                    {opt.text}
                  </Button>
                ))}
              </div>
            </motion.div>
          ) : (
            <motion.div
              initial={{ opacity: 0 }}
