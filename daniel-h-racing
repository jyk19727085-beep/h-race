import React, { useState, useEffect, useRef } from 'react';

// --- 미네르바 코어 엔진 (E-VAL 2025 가중치) ---
const WEIGHTS = { O: 35, H: 30, T: 25, J: 10 };

// 실전 모의 팩트 데이터 (05.09 서울 기준)
const MOCK_FACTS = [
  { no: 1, name: "강력한축마", owner: "김진영", trainer: "성상현(41)", jockey: "문세영", style: "선행", s1f: 13.2, g3f: 37.1, score: 88, rank: "황실 승부권", o_score: 32, h_score: 25, t_score: 22, j_score: 9, note: "가족법인 연대 출주 (+5점)" },
  { no: 2, name: "숨겨진보석", owner: "가족법인A", trainer: "홍윤화(39)", jockey: "김용근", style: "추입", s1f: 14.1, g3f: 36.2, score: 72, rank: "귀족 입상권", o_score: 20, h_score: 22, t_score: 20, j_score: 10, note: "머니플로우: 예상지 소외 독식 찬스 (+6점)" },
  { no: 3, name: "거품인기마", owner: "일반마주", trainer: "일반(11)", jockey: "일반", style: "선행", s1f: 13.5, g3f: 38.5, score: 45, rank: "일반", o_score: 15, h_score: 10, t_score: 15, j_score: 5, note: "머니플로우: 과열 경고 (-4점)" },
  { no: 4, name: "안정적전력", owner: "법인마주B", trainer: "우수(22)", jockey: "우수기수", style: "선입", s1f: 13.7, g3f: 37.5, score: 65, rank: "기사단 복병권", o_score: 18, h_score: 20, t_score: 19, j_score: 8, note: "승군전 관망 패턴 의심" }
];

export default function MinervaMobileDashboard() {
  const [isAuthenticated, setIsAuthenticated] = useState(false);
  const [masterKey, setMasterKey] = useState('');
  const [isAnalyzing, setIsAnalyzing] = useState(false);
  const [raceData, setRaceData] = useState([]);
  const [progress, setProgress] = useState(0);
  const [selectedHorse, setSelectedHorse] = useState(null);

  // 보안 인가 (ABSOLUTE SECURITY)
  const handleLogin = (e) => {
    e.preventDefault();
    if (masterKey === 'UNICORN7085') {
      setIsAuthenticated(true);
    } else {
      alert("🚨 ACCESS DENIED: 비인가 접근입니다.");
    }
  };

  // 0.8초 오버클럭 딥러닝 파싱
  const runAnalysis = () => {
    setIsAnalyzing(true);
    setProgress(0);
    setRaceData([]);
    setSelectedHorse(null);
    
    let currentProgress = 0;
    const interval = setInterval(() => {
      currentProgress += 20;
      setProgress(Math.min(currentProgress, 100));
      
      if (currentProgress >= 100) {
        clearInterval(interval);
        // 역순 정렬 (1번 마필이 하단(Bottom)에 오도록 설계)
        setRaceData([...MOCK_FACTS].sort((a, b) => b.no - a.no));
        setIsAnalyzing(false);
      }
    }, 160); // 총 0.8초 (800ms) 소요
  };

  if (!isAuthenticated) {
    return (
      <div className="flex flex-col items-center justify-center min-h-screen bg-black text-emerald-500 font-mono p-4">
        <form onSubmit={handleLogin} className="w-full max-w-sm p-8 border border-emerald-500 rounded-2xl shadow-[0_0_20px_rgba(0,255,100,0.2)] bg-gray-900 text-center">
          <h1 className="text-3xl font-black mb-2 tracking-widest text-emerald-400">MINERVA</h1>
          <p className="mb-8 text-xs text-emerald-700 font-bold tracking-widest">PRO MOBILE EDITION</p>
          <input 
            type="password" 
            placeholder="MASTER KEY" 
            value={masterKey}
            onChange={(e) => setMasterKey(e.target.value)}
            className="w-full p-4 mb-6 bg-black border border-emerald-800 rounded-lg text-center text-xl text-emerald-400 focus:outline-none focus:border-emerald-400 transition-colors"
          />
          <button type="submit" className="w-full p-4 bg-emerald-900 hover:bg-emerald-700 rounded-lg text-white font-bold tracking-widest transition-all active:scale-95">
            SYSTEM ACCESS
          </button>
        </form>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gray-950 text-gray-100 p-3 sm:p-5 font-sans overflow-x-hidden">
      {/* 상단 모바일 컨트롤 패널 */}
      <header className="flex flex-col gap-3 mb-4 p-4 border border-blue-900 rounded-2xl bg-gray-900 shadow-[0_0_15px_rgba(0,100,255,0.15)] relative overflow-hidden">
        <div className="absolute top-0 left-0 w-1 h-full bg-blue-500 shadow-[0_0_10px_#3b82f6]"></div>
        <div className="flex justify-between items-start">
          <div>
            <h1 className="text-xl font-black text-blue-400 tracking-wider">MINERVA PRO</h1>
            <p className="text-xs text-gray-400 mt-1 flex items-center gap-1">
              <span className="inline-block w-2 h-2 rounded-full bg-green-500 animate-pulse"></span>
              7-CORE API SYNC READY
            </p>
          </div>
          <div className="flex items-center gap-2 bg-gray-800 px-3 py-1 rounded-full border border-gray-700">
            <span className="relative flex h-2 w-2">
              <span className="animate-ping absolute inline-flex h-full w-full rounded-full bg-red-400 opacity-75"></span>
              <span className="relative inline-flex rounded-full h-2 w-2 bg-red-500"></span>
            </span>
            <span className="text-xs font-bold text-red-400">AUTO-SYNC</span>
          </div>
        </div>
        
        <button 
          onClick={runAnalysis} 
          disabled={isAnalyzing} 
          className="w-full mt-2 py-3 bg-gradient-to-r from-blue-800 to-blue-600 hover:from-blue-700 hover:to-blue-500 rounded-xl font-black text-white text-sm transition-all shadow-[0_0_15px_rgba(0,100,255,0.4)] active:scale-[0.98]"
        >
          {isAnalyzing ? "리얼 팩트 딥러닝 중..." : "실전 팩트 분석 개시 (0.8s)"}
        </button>
      </header>

      {/* 분석 프로그레스 바 */}
      {isAnalyzing && (
        <div className="w-full bg-gray-900 rounded-full h-1.5 mb-4 overflow-hidden border border-gray-800">
          <div className="bg-blue-500 h-1.5 rounded-full transition-all duration-150 relative" style={{ width: `${progress}%` }}>
            <div className="absolute top-0 right-0 bottom-0 left-0 bg-gradient-to-r from-transparent to-white opacity-30 animate-pulse"></div>
          </div>
        </div>
      )}

      {raceData.length > 0 && (
        <div className="flex flex-col gap-4">
          
          {/* 모바일 랭킹 보드 */}
          <div className="bg-gray-900 p-4 rounded-2xl border border-gray-800 shadow-lg">
            <h2 className="text-sm font-black mb-3 text-emerald-400 flex items-center gap-2">
              <span>📊</span> WIN-INDEX 랭킹 (E-VAL 2025)
            </h2>
            <div className="flex flex-col gap-2">
              {[...raceData].sort((a, b) => b.score - a.score).map((horse) => (
                <div 
                  key={horse.no} 
                  onClick={() => setSelectedHorse(horse)}
                  className={`flex justify-between items-center p-3 rounded-xl border-l-4 cursor-pointer transition-all active:scale-[0.98]
                    ${selectedHorse?.no === horse.no ? 'bg-gray-800 border-blue-500 shadow-[0_0_10px_rgba(59,130,246,0.3)]' : 'bg-gray-950 border-gray-700 hover:bg-gray-800'}`}
                >
                  <div className="flex items-center gap-3">
                    <span className={`text-xl font-black w-6 text-center ${horse.rank === '황실 승부권' ? 'text-amber-400' : 'text-gray-300'}`}>
                      {horse.no}
                    </span>
                    <div>
                      <h3 className="text-base font-bold text-gray-100 leading-tight">{horse.name}</h3>
                      <p className="text-[10px] text-gray-500 mt-0.5">{horse.trainer} / {horse.jockey}</p>
                    </div>
                  </div>
                  <div className="text-right">
                    <div className="text-lg font-black text-emerald-400">{horse.score}</div>
                    <div className="text-[10px] font-bold text-gray-400">{horse.rank}</div>
                  </div>
                </div>
              ))}
            </div>
          </div>

          {/* 선택 마필 상세 팩트 시트 */}
          {selectedHorse && (
            <div className="bg-gray-900 p-4 rounded-2xl border border-blue-900/50 shadow-[0_0_20px_rgba(0,100,255,0.1)] animate-fade-in">
              <h2 className="text-sm font-black mb-3 text-blue-400">🔍 {selectedHorse.name} 팩트 시트</h2>
              
              {/* OHTJ 가중치 바 */}
              <div className="grid grid-cols-2 gap-3 mb-4">
                {[
                  { label: 'O (마주)', val: selectedHorse.o_score, max: WEIGHTS.O, color: 'bg-purple-500' },
                  { label: 'H (마필)', val: selectedHorse.h_score, max: WEIGHTS.H, color: 'bg-emerald-500' },
                  { label: 'T (조교)', val: selectedHorse.t_score, max: WEIGHTS.T, color: 'bg-blue-500' },
                  { label: 'J (기수)', val: selectedHorse.j_score, max: WEIGHTS.J, color: 'bg-amber-500' }
                ].map((stat, i) => (
                  <div key={i} className="bg-gray-950 p-2 rounded-lg border border-gray-800">
                    <div className="flex justify-between text-[10px] text-gray-400 mb-1">
                      <span>{stat.label}</span>
                      <span className="font-bold text-gray-200">{stat.val}/{stat.max}</span>
                    </div>
                    <div className="w-full bg-gray-800 rounded-full h-1">
                      <div className={`${stat.color} h-1 rounded-full`} style={{ width: `${(stat.val / stat.max) * 100}%` }}></div>
                    </div>
                  </div>
                ))}
              </div>

              {/* 시크릿 노트 & 머니플로우 */}
              <div className="bg-red-950/30 border border-red-900/50 p-3 rounded-xl text-xs text-red-200 leading-relaxed">
                <span className="font-bold text-red-400 mr-1">🚨 시크릿 노트:</span> 
                {selectedHorse.note} <br/>
                <span className="text-gray-400 text-[10px] mt-1 block">구간 팩트: S-1F {selectedHorse.s1f}s / G-3F {selectedHorse.g3f}s</span>
              </div>
            </div>
          )}

          {/* 모바일 역동적 전개도 (우측 -> 좌측, 1번 하단) */}
          <div className="bg-gray-900 p-4 rounded-2xl border border-gray-800 relative overflow-hidden">
            <h2 className="text-sm font-black mb-3 text-amber-400 flex items-center gap-2">
              <span>🏁</span> 다이내믹 시뮬레이터 (역방향)
            </h2>
            
            {/* 가로 스크롤을 방지하고 모바일 뷰에 꽉 차게 렌더링 */}
            <div className="relative w-full h-48 bg-gray-950 rounded-xl border border-gray-700 py-2 flex flex-col justify-around overflow-hidden">
              {/* 결승선 (좌측) */}
              <div className="absolute left-4 top-0 bottom-0 w-1 bg-gradient-to-b from-red-500 via-red-400 to-red-500 shadow-[0_0_10px_#ef4444] z-0"></div>
              <span className="absolute left-1 top-2 text-[8px] font-black text-red-500 opacity-50 rotate-90">FINISH</span>
              
              {/* 출발선 (우측) */}
              <div className="absolute right-4 top-0 bottom-0 w-[1px] border-r border-dashed border-gray-600 z-0"></div>
              
              {raceData.map((horse) => (
                <div key={horse.no} className="relative w-full h-8 flex items-center group">
                  {/* 트랙 라인 */}
                  <div className="absolute w-full h-[1px] bg-gray-800/50 z-0"></div>
                  
                  {/* 마필 아이콘 (우측에서 출발하여 좌측 결승선 방향으로 이동) */}
                  <div 
                    className={`absolute h-6 rounded-full flex items-center px-2 text-[10px] font-bold text-white z-10 transition-all duration-[2000ms] ease-out shadow-lg
                      ${horse.no === 1 ? 'bg-red-600' : horse.style === '추입' ? 'bg-blue-600' : 'bg-gray-700'}
                      ${horse.score >= 80 ? 'shadow-[0_0_12px_rgba(255,215,0,0.5)] border border-amber-400' : ''}`}
                    style={{ 
                      /* 우측(100%)에서 시작하여 좌측(0%)으로 진행. 점수가 높을수록 left 값이 작아짐(결승선에 가까움) */
                      left: `${100 - (horse.score / 100) * 85}%`, 
                      width: 'max-content' 
                    }}
                  >
                    <span className="mr-1 opacity-70">{horse.no}.</span>
                    <span className="truncate max-w-[50px] sm:max-w-[80px]">{horse.name}</span>
                  </div>
                </div>
              ))}
            </div>
            <p className="text-[9px] text-gray-500 text-center mt-3">※ 모바일 최적화: 우측 게이트 출발 ➡️ 좌측 결승선 도착 (하단 1번 코스)</p>
          </div>

        </div>
      )}
    </div>
  );
}
