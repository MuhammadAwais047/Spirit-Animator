import React, { useState, useEffect, useRef, useCallback } from 'react';
import { Play, Pause, Code, Image as ImageIcon, Settings, Move, Grid3X3, Copy, Check, Plus, Trash2, Layers, Sparkles, Bot, Wand2, Loader, Video, Eye, MousePointer2, Palette, Maximize2, Download, Ruler, SlidersHorizontal, Upload, FileJson, FlipHorizontal, Keyboard } from 'lucide-react';

const SpriteAnimator = () => {
  // --- Gemini API Setup ---
  const apiKey = ""; // API Key injected by environment

  // --- State ---
  const [imageSrc, setImageSrc] = useState('player.png'); 
  const [imageDimensions, setImageDimensions] = useState({ width: 0, height: 0 });
  
  // Global Grid Config
  const [baseWidth, setBaseWidth] = useState(48);
  const [baseHeight, setBaseHeight] = useState(48);
  const [globalOffsetX, setGlobalOffsetX] = useState(0);
  const [globalOffsetY, setGlobalOffsetY] = useState(0);
  const [gapX, setGapX] = useState(0); 
  const [gapY, setGapY] = useState(0); 

  // Animation States System
  const [states, setStates] = useState([
    { id: 'idle', name: 'Idle', frames: [0, 1, 2, 3], fps: 8, customWidth: null, customHeight: null, flipX: false },
    { id: 'run', name: 'Run', frames: [4, 5, 6, 7], fps: 12, customWidth: null, customHeight: null, flipX: false },
    { id: 'dash', name: 'Dash', frames: [8, 9], fps: 15, customWidth: 96, customHeight: null, flipX: false } 
  ]);
  const [activeStateId, setActiveStateId] = useState('idle');

  // Playback State
  const [isPlaying, setIsPlaying] = useState(true);
  const [currentFrame, setCurrentFrame] = useState(0);
  const [scale, setScale] = useState(4);
  const [onionSkin, setOnionSkin] = useState(false); 
  
  // View & Preview Adjustment State
  const [pan, setPan] = useState({ x: 0, y: 0 });
  const [isPanning, setIsPanning] = useState(false);
  const [bgType, setBgType] = useState('dark'); 
  
  // Mapping Mode State
  const [isMappingMode, setIsMappingMode] = useState(false);
  const [syncGridToState, setSyncGridToState] = useState(false); 

  // Recording State
  const [isRecording, setIsRecording] = useState(false);
  const [autoRecordStateId, setAutoRecordStateId] = useState(null); 
  const mediaRecorderRef = useRef(null);
  const chunksRef = useRef([]);
  
  // UI State
  const [showGrid, setShowGrid] = useState(true);
  const [showGridTuner, setShowGridTuner] = useState(false); 
  const [activeTab, setActiveTab] = useState('preview');
  const [copyFeedback, setCopyFeedback] = useState(null);
  const [showShortcuts, setShowShortcuts] = useState(false);
  const [isDragging, setIsDragging] = useState(false); // For drag-and-drop

  // AI State
  const [aiTargetEngine, setAiTargetEngine] = useState('Unity (C#)');
  const [aiCodeResult, setAiCodeResult] = useState('');
  const [isGeneratingCode, setIsGeneratingCode] = useState(false);
  const [aiAnalysisResult, setAiAnalysisResult] = useState('');
  const [isAnalyzing, setIsAnalyzing] = useState(false);

  // Refs
  const canvasRef = useRef(null);
  const requestRef = useRef();
  const frameCountRef = useRef(0);
  const sequenceIndexRef = useRef(0);
  const imageRef = useRef(new Image());
  const lastMousePos = useRef({ x: 0, y: 0 });
  const loopCounterRef = useRef(0);
  const dropZoneRef = useRef(null);

  // Derived State
  const activeState = states.find(s => s.id === activeStateId) || states[0];

  // --- Initialization ---
  useEffect(() => {
    const img = imageRef.current;
    img.src = imageSrc;
    img.onload = () => {
      setImageDimensions({ width: img.naturalWidth, height: img.naturalHeight });
    };
  }, [imageSrc]);

  // --- Keyboard Shortcuts ---
  useEffect(() => {
    const handleKeyDown = (e) => {
        // Ignore shortcuts if user is typing in an input field
        if (e.target.tagName === 'INPUT' || e.target.tagName === 'TEXTAREA') return;

        switch(e.code) {
            case 'Space':
                e.preventDefault();
                setIsPlaying(prev => !prev);
                break;
            case 'ArrowRight':
                e.preventDefault();
                setIsPlaying(false);
                stepFrame(1);
                break;
            case 'ArrowLeft':
                e.preventDefault();
                setIsPlaying(false);
                stepFrame(-1);
                break;
            case 'KeyM':
                setIsMappingMode(prev => !prev);
                break;
            default:
                break;
        }
    };
    window.addEventListener('keydown', handleKeyDown);
    return () => window.removeEventListener('keydown', handleKeyDown);
  }, [activeState]); // Depend on activeState to ensure stepFrame has fresh data

  // --- Helper: Step Frame Manually ---
  const stepFrame = (direction) => {
      if (!activeState || activeState.frames.length === 0) return;
      
      let nextIndex = sequenceIndexRef.current + direction;
      if (nextIndex >= activeState.frames.length) nextIndex = 0;
      if (nextIndex < 0) nextIndex = activeState.frames.length - 1;
      
      sequenceIndexRef.current = nextIndex;
      setCurrentFrame(activeState.frames[nextIndex]);
  };


  // --- Animation Loop ---
  const animate = (time) => {
    const shouldPlay = isPlaying || autoRecordStateId;

    if (shouldPlay && activeState && activeState.frames.length > 0) {
      frameCountRef.current++;
      const frameInterval = 60 / activeState.fps;
      
      if (frameCountRef.current >= frameInterval) {
        const nextIndex = (sequenceIndexRef.current + 1);
        if (nextIndex >= activeState.frames.length) {
            sequenceIndexRef.current = 0;
            loopCounterRef.current++;
            if (autoRecordStateId) stopAutoRecord();
        } else {
            sequenceIndexRef.current = nextIndex;
        }
        setCurrentFrame(activeState.frames[sequenceIndexRef.current]);
        frameCountRef.current = 0;
      }
    }
    requestRef.current = requestAnimationFrame(animate);
  };

  useEffect(() => {
    requestRef.current = requestAnimationFrame(animate);
    return () => cancelAnimationFrame(requestRef.current);
  }, [isPlaying, activeState, autoRecordStateId]); 

  // Safety Check for Empty States
  useEffect(() => {
    if (activeState) {
      if (activeState.frames.length > 0) {
        sequenceIndexRef.current = 0;
        setCurrentFrame(activeState.frames[0]);
      } else {
        setCurrentFrame(null); // Valid empty state handling
      }
      frameCountRef.current = 0;
    }
  }, [activeStateId]);

  // --- Rendering ---
  useEffect(() => {
    const canvas = canvasRef.current;
    if (!canvas || !imageDimensions.width) return;
    
    const ctx = canvas.getContext('2d');
    ctx.imageSmoothingEnabled = false;
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    // Safety: If no frames, don't draw
    if (currentFrame === null && !onionSkin) return;

    // Determine dimensions for CURRENT active state
    const frameWidth = activeState.customWidth || baseWidth;
    const frameHeight = activeState.customHeight || baseHeight;
    
    const strideX = baseWidth + gapX;
    const cols = Math.floor(imageDimensions.width / strideX) || 1;

    const drawFrame = (frameIdx, alpha = 1, isGhost = false) => {
        if (frameIdx === undefined || frameIdx === null) return { drawX: 0, drawY: 0 };

        const colIndex = frameIdx % cols;
        const rowIndex = Math.floor(frameIdx / cols);
        const strideY = baseHeight + gapY;

        // Source position
        const sx = (colIndex * strideX) + globalOffsetX;
        const sy = (rowIndex * strideY) + globalOffsetY;

        // Destination Position
        // We need to handle Flipping here.
        // To flip around center: Translate to center, Scale -1, Translate back.
        
        const centerX = canvas.width / 2 + pan.x;
        const centerY = canvas.height / 2 + pan.y;
        
        const destW = frameWidth * scale;
        const destH = frameHeight * scale;

        ctx.save();
        ctx.globalAlpha = alpha;
        
        // Apply Flip if active and NOT a ghost (or if ghost should also flip? typically yes)
        // We only flip if the State says so
        if (activeState.flipX) {
             ctx.translate(centerX, centerY);
             ctx.scale(-1, 1);
             ctx.translate(-centerX, -centerY);
        }

        // Draw Image
        ctx.drawImage(
            imageRef.current,
            sx, sy, frameWidth, frameHeight, 
            centerX - (destW / 2), centerY - (destH / 2), destW, destH
        );

        ctx.restore();
        
        return { 
            drawX: centerX - (destW / 2), 
            drawY: centerY - (destH / 2),
            w: destW,
            h: destH
        };
    };

    // 1. Onion Skin
    if (onionSkin && activeState.frames.length > 0 && !autoRecordStateId) {
        drawFrame(activeState.frames[0], 0.3, true);
    }

    // 2. Current Frame
    const { drawX, drawY, w, h } = drawFrame(currentFrame, 1.0);

    // 3. Debug Box (Visual Guide only)
    if (showGrid && !autoRecordStateId && currentFrame !== null) {
      ctx.strokeStyle = 'rgba(0, 255, 100, 0.6)';
      ctx.lineWidth = 2;
      ctx.strokeRect(drawX, drawY, w, h);
    }
    
    // 4. Recording Indicator
    if (isRecording || autoRecordStateId) {
        ctx.fillStyle = 'red';
        ctx.beginPath();
        ctx.arc(20, 20, 6, 0, Math.PI * 2);
        ctx.fill();
    }

  }, [currentFrame, baseWidth, baseHeight, gapX, gapY, globalOffsetX, globalOffsetY, scale, showGrid, onionSkin, imageDimensions, activeState, isRecording, pan, autoRecordStateId]);

  // --- Preview Interactions ---
  const handleMouseDown = (e) => {
      setIsPanning(true);
      lastMousePos.current = { x: e.clientX, y: e.clientY };
  };

  const handleMouseMove = (e) => {
      if (!isPanning) return;
      const dx = e.clientX - lastMousePos.current.x;
      const dy = e.clientY - lastMousePos.current.y;
      setPan(prev => ({ x: prev.x + dx, y: prev.y + dy }));
      lastMousePos.current = { x: e.clientX, y: e.clientY };
  };

  const handleMouseUp = () => setIsPanning(false);

  // --- Drag and Drop ---
  const handleDragOver = (e) => { e.preventDefault(); setIsDragging(true); };
  const handleDragLeave = (e) => { e.preventDefault(); setIsDragging(false); };
  const handleDrop = (e) => {
      e.preventDefault();
      setIsDragging(false);
      const file = e.dataTransfer.files[0];
      if (file && file.type.startsWith('image/')) {
          const reader = new FileReader();
          reader.onload = (evt) => setImageSrc(evt.target.result);
          reader.readAsDataURL(file);
      }
  };

  // --- State Management Helpers ---
  const updateActiveState = (key, value) => {
    setStates(prev => prev.map(s => s.id === activeStateId ? { ...s, [key]: value } : s));
  };

  const handleSequenceChange = (str) => {
    const nums = str.split(',').map(s => parseInt(s.trim())).filter(n => !isNaN(n));
    updateActiveState('frames', nums);
  };

  const toggleFrameInSequence = (frameId) => {
      if (!activeState) return;
      const idx = activeState.frames.indexOf(frameId);
      let newFrames;
      if (idx >= 0) newFrames = activeState.frames.filter(f => f !== frameId);
      else newFrames = [...activeState.frames, frameId];
      updateActiveState('frames', newFrames);
  };

  const addNewState = () => { 
      const newId = `state_${Date.now()}`; 
      setStates([...states, { id: newId, name: 'New State', frames: [0], fps: 8, customWidth: null, customHeight: null, flipX: false }]); 
      setActiveStateId(newId); 
  };

  const deleteState = (id) => { 
      if (states.length > 1) { 
          const remaining = states.filter(s => s.id !== id); 
          setStates(remaining); 
          if (activeStateId === id) setActiveStateId(remaining[0].id); 
      } 
  };

  // --- Save & Load Project ---
  const saveProject = () => {
      const projectData = {
          version: 1,
          timestamp: Date.now(),
          imageSrc, // Note: Base64 strings can be large, but OK for local JSON
          config: { baseWidth, baseHeight, globalOffsetX, globalOffsetY, gapX, gapY },
          states
      };
      const blob = new Blob([JSON.stringify(projectData, null, 2)], { type: 'application/json' });
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url;
      a.download = `animator_project_${Date.now()}.json`;
      a.click();
      URL.revokeObjectURL(url);
  };

  const loadProject = (e) => {
      const file = e.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = (evt) => {
          try {
              const data = JSON.parse(evt.target.result);
              if (data.imageSrc) setImageSrc(data.imageSrc);
              if (data.config) {
                  setBaseWidth(data.config.baseWidth);
                  setBaseHeight(data.config.baseHeight);
                  setGlobalOffsetX(data.config.globalOffsetX || 0);
                  setGlobalOffsetY(data.config.globalOffsetY || 0);
                  setGapX(data.config.gapX || 0);
                  setGapY(data.config.gapY || 0);
              }
              if (data.states) {
                  setStates(data.states);
                  setActiveStateId(data.states[0]?.id || 'idle');
              }
          } catch (err) {
              alert("Failed to load project file.");
          }
      };
      reader.readAsText(file);
  };

  // --- Recording Logic ---
  const startAutoRecord = (stateId) => {
      setActiveStateId(stateId);
      setIsPlaying(false); 
      sequenceIndexRef.current = 0;
      const targetState = states.find(s => s.id === stateId);
      if(targetState && targetState.frames.length > 0) setCurrentFrame(targetState.frames[0]);
      loopCounterRef.current = 0;

      setTimeout(() => { 
          const stream = canvasRef.current.captureStream(30);
          mediaRecorderRef.current = new MediaRecorder(stream, { mimeType: 'video/webm' });
          chunksRef.current = [];
          mediaRecorderRef.current.ondataavailable = (e) => { if (e.data.size > 0) chunksRef.current.push(e.data); };
          
          mediaRecorderRef.current.onstop = () => {
                const blob = new Blob(chunksRef.current, { type: 'video/webm' });
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url; 
                a.download = `${targetState.name}_anim.webm`; 
                a.click(); 
                URL.revokeObjectURL(url);
                setAutoRecordStateId(null); 
          };
          
          mediaRecorderRef.current.start();
          setAutoRecordStateId(stateId); 
      }, 100);
  };

  const stopAutoRecord = () => {
      if (mediaRecorderRef.current && mediaRecorderRef.current.state !== 'inactive') {
          mediaRecorderRef.current.stop();
      }
  };

  const toggleManualRecording = () => {
    if (isRecording) {
        mediaRecorderRef.current.stop(); setIsRecording(false);
    } else {
        const stream = canvasRef.current.captureStream(30);
        mediaRecorderRef.current = new MediaRecorder(stream, { mimeType: 'video/webm' });
        chunksRef.current = [];
        mediaRecorderRef.current.ondataavailable = (e) => { if (e.data.size > 0) chunksRef.current.push(e.data); };
        mediaRecorderRef.current.onstop = () => { const blob = new Blob(chunksRef.current, { type: 'video/webm' }); const url = URL.createObjectURL(blob); const a = document.createElement('a'); a.href = url; a.download = `animation_${activeState.name}.webm`; a.click(); URL.revokeObjectURL(url); };
        mediaRecorderRef.current.start(); setIsRecording(true);
    }
  };

  // --- AI & Export ---
  const generateJS = () => {
    const stateConfigObj = states.reduce((acc, s) => { 
        acc[s.name.replace(/\s+/g, '')] = { 
            frames: s.frames, fps: s.fps, w: s.customWidth || baseWidth, h: s.customHeight || baseHeight,
            gapX, gapY, flipX: s.flipX
        }; 
        return acc; 
    }, {});
    return `// Config with Flip & Gap Support\nconst playerConfig = {\n  src: '${imageSrc.substring(0, 15)}...',\n  baseWidth: ${baseWidth},\n  baseHeight: ${baseHeight},\n  gapX: ${gapX},\n  gapY: ${gapY},\n  states: ${JSON.stringify(stateConfigObj, null, 2)}\n};`;
  };

  const handleAIExport = async () => {
    setIsGeneratingCode(true); setAiCodeResult('');
    const configSummary = { baseWidth, baseHeight, gapX, gapY, states: states.map(s => ({ name: s.name, frames: s.frames, fps: s.fps, w: s.customWidth, h: s.customHeight, flipX: s.flipX })) };
    const prompt = `Act as an expert game developer. Generate a production-ready ${aiTargetEngine} script. KEY REQUIREMENTS: Support gaps (gapX, gapY) and Horizontal Flipping (flipX). Config: ${JSON.stringify(configSummary)}. Only provide the code.`;
    try {
      const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
        method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify({ contents: [{ parts: [{ text: prompt }] }] })
      });
      const data = await response.json();
      setAiCodeResult((data.candidates?.[0]?.content?.parts?.[0]?.text || "Error generating code.").replace(/```\w*\n/g, '').replace(/```/g, ''));
    } catch (error) { setAiCodeResult("// Error calling Gemini API."); } finally { setIsGeneratingCode(false); }
  };

  const handleAIAnalysis = async () => {
    setIsAnalyzing(true); setAiAnalysisResult('');
    let base64Data = "";
    if (imageSrc.startsWith('data:')) base64Data = imageSrc.split(',')[1];
    else {
        try {
            const resp = await fetch(imageSrc); const blob = await resp.blob();
            base64Data = await new Promise(r => { const reader = new FileReader(); reader.onloadend = () => r(reader.result.split(',')[1]); reader.readAsDataURL(blob); });
        } catch (e) { setAiAnalysisResult("Could not load image."); setIsAnalyzing(false); return; }
    }
    const prompt = `Analyze this sprite sheet. 1. Describe character. 2. Suggest dimensions and gap size (if any).`;
    try {
      const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
        method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify({ contents: [{ parts: [{ text: prompt }, { inlineData: { mimeType: "image/png", data: base64Data } }] }] })
      });
      const data = await response.json();
      setAiAnalysisResult(data.candidates?.[0]?.content?.parts?.[0]?.text || "Could not analyze image.");
    } catch (error) { setAiAnalysisResult("Error calling Gemini Vision API."); } finally { setIsAnalyzing(false); }
  };

  const copyToClipboard = (text, type) => { navigator.clipboard.writeText(text); setCopyFeedback(type); setTimeout(() => setCopyFeedback(null), 2000); };

  // --- Helper Components ---
  const GridOverlay = () => {
    if (!imageDimensions.width) return null;
    
    const useStateSize = syncGridToState && (activeState.customWidth || activeState.customHeight);
    
    const gWidth = useStateSize ? (activeState.customWidth || baseWidth) : baseWidth;
    const gHeight = useStateSize ? (activeState.customHeight || baseHeight) : baseHeight;
    
    const strideX = gWidth + gapX;
    const strideY = gHeight + gapY;
    
    const cols = Math.floor(imageDimensions.width / strideX) || 1;
    const rows = Math.floor(imageDimensions.height / strideY) || 1;
    
    const capW = activeState.customWidth || baseWidth;
    const capH = activeState.customHeight || baseHeight;

    return (
        <div className={`absolute top-0 left-0 border border-blue-500/20 ${isMappingMode ? 'cursor-crosshair' : 'pointer-events-none'}`} style={{ width: imageDimensions.width, height: imageDimensions.height }}>
            {/* Base Grid */}
            {showGrid && Array.from({ length: rows }).map((_, r) => (Array.from({ length: cols }).map((_, c) => {
                const idx = r * cols + c;
                const isInSequence = activeState.frames.includes(idx);
                const isCurrent = idx === currentFrame;
                
                const left = (c * strideX) + globalOffsetX;
                const top = (r * strideY) + globalOffsetY;

                return (
                  <div key={idx} onClick={() => isMappingMode && toggleFrameInSequence(idx)} 
                       className={`absolute box-border transition-all 
                       ${isCurrent ? 'border-red-500 bg-red-500/30 z-20 border-2' : isInSequence ? 'border-emerald-500/50 bg-emerald-500/20 border' : isMappingMode ? 'border-slate-700/30 hover:bg-white/10 border' : 'border-slate-700/30 border'}`}
                      style={{ width: gWidth, height: gHeight, left, top }}>
                      <span className={`text-[8px] px-1 absolute top-0 left-0 pointer-events-none ${isInSequence ? 'text-emerald-300 bg-emerald-900/80' : 'text-slate-500'}`}>{idx}</span>
                      {isInSequence && (<div className="absolute bottom-0 right-0 bg-emerald-600 text-white text-[8px] px-1 rounded-tl-sm pointer-events-none">#{activeState.frames.indexOf(idx) + 1}</div>)}
                  </div>
                )
            })))}
             
             {!useStateSize && (activeState.customWidth || activeState.customHeight) && (
                 <div className="absolute border-2 border-dashed border-orange-400 z-30 box-content animate-pulse pointer-events-none"
                 style={{ 
                     width: capW, height: capH, 
                     left: ((currentFrame % Math.floor(imageDimensions.width/(baseWidth+gapX))) * (baseWidth+gapX)) + globalOffsetX, 
                     top: (Math.floor(currentFrame / Math.floor(imageDimensions.width/(baseWidth+gapX))) * (baseHeight+gapY)) + globalOffsetY 
                 }} />
            )}
        </div>
    )
  }

  return (
    <div 
        className={`flex flex-col h-screen bg-slate-950 text-slate-100 font-sans overflow-hidden ${isDragging ? 'opacity-50' : ''}`}
        onDragOver={handleDragOver}
        onDragLeave={handleDragLeave}
        onDrop={handleDrop}
    >
      {/* Overlay for Dragging */}
      {isDragging && (
          <div className="absolute inset-0 z-50 flex items-center justify-center bg-indigo-600/30 backdrop-blur-sm pointer-events-none border-4 border-indigo-400 border-dashed m-4 rounded-3xl">
              <div className="text-3xl font-bold text-white flex flex-col items-center gap-4">
                  <Upload className="w-16 h-16" />
                  Drop Image to Load
              </div>
          </div>
      )}

      {/* Responsive Header */}
      <header className="bg-slate-900 border-b border-slate-800 p-3 md:p-4 flex flex-col md:flex-row md:items-center justify-between shadow-md z-10 gap-2 md:gap-0">
        <div className="flex items-center gap-3">
            <div className="p-2 bg-indigo-600 rounded-lg shadow-indigo-500/20 shadow-lg"><Grid3X3 className="w-6 h-6 text-white" /></div>
            <div>
                <h1 className="font-bold text-xl tracking-tight text-white">Sprite Animator <span className="text-indigo-400">Pro</span></h1>
                <p className="text-xs text-slate-400 flex items-center gap-2">
                    Visual Mapper & AI Lab 
                    <button onClick={() => setShowShortcuts(!showShortcuts)} className="hover:text-indigo-300"><Keyboard className="w-3 h-3 inline" /></button>
                </p>
            </div>
        </div>
        
        {/* Shortcut Popup */}
        {showShortcuts && (
            <div className="absolute top-16 left-4 z-50 bg-slate-800 border border-slate-700 p-4 rounded-lg shadow-2xl text-xs space-y-2 animate-in slide-in-from-top-2 w-64">
                <h4 className="font-bold text-white mb-2 border-b border-slate-700 pb-1">Keyboard Shortcuts</h4>
                <div className="flex justify-between"><span className="text-slate-400">Play/Pause</span> <span className="text-indigo-300 font-mono bg-slate-900 px-1 rounded">Space</span></div>
                <div className="flex justify-between"><span className="text-slate-400">Next Frame</span> <span className="text-indigo-300 font-mono bg-slate-900 px-1 rounded">→</span></div>
                <div className="flex justify-between"><span className="text-slate-400">Prev Frame</span> <span className="text-indigo-300 font-mono bg-slate-900 px-1 rounded">←</span></div>
                <div className="flex justify-between"><span className="text-slate-400">Toggle Mapper</span> <span className="text-indigo-300 font-mono bg-slate-900 px-1 rounded">M</span></div>
                <div className="text-[10px] text-slate-500 mt-2 pt-2 border-t border-slate-700">Click outside to close not implemented, toggle icon again.</div>
            </div>
        )}

        <div className="flex items-center gap-2 self-end md:self-auto">
             <button onClick={saveProject} className="flex items-center gap-2 bg-slate-800 hover:bg-slate-700 border border-slate-700 px-3 py-2 rounded-lg transition text-sm font-medium" title="Save Project JSON">
                <Download className="w-4 h-4 text-green-400" /> <span className="hidden md:inline">Save Project</span>
             </button>
             <label className="flex items-center gap-2 cursor-pointer bg-slate-800 hover:bg-slate-700 border border-slate-700 px-3 py-2 rounded-lg transition text-sm font-medium" title="Load Project JSON">
                <FileJson className="w-4 h-4 text-blue-400" /> <span className="hidden md:inline">Load</span>
                <input type="file" accept=".json" className="hidden" onChange={loadProject} />
             </label>
             <div className="w-[1px] h-6 bg-slate-700 mx-2"></div>
             <label className="flex items-center gap-2 cursor-pointer bg-indigo-600 hover:bg-indigo-500 border border-indigo-500 px-4 py-2 rounded-lg transition text-sm font-medium shadow-lg shadow-indigo-500/20">
                <ImageIcon className="w-4 h-4 text-white" /><span>New Image</span>
                <input type="file" accept="image/*" className="hidden" onChange={(e) => { const file = e.target.files[0]; if(file){ const reader = new FileReader(); reader.onload = (evt) => setImageSrc(evt.target.result); reader.readAsDataURL(file); } }} />
            </label>
        </div>
      </header>

      {/* Responsive Main Layout */}
      <div className="flex flex-col md:flex-row flex-1 overflow-hidden">
        
        {/* Sidebar */}
        <aside className="w-full md:w-80 bg-slate-900 border-r border-slate-800 flex flex-col md:h-full overflow-y-auto scrollbar-thin scrollbar-thumb-slate-700 order-2 md:order-1 max-h-[40vh] md:max-h-full border-t md:border-t-0 border-slate-800">
            <div className="p-5 border-b border-slate-800">
                <div className="flex items-center gap-2 mb-4 text-indigo-400 font-bold text-xs uppercase tracking-wider"><Settings className="w-3 h-3" /> Base Grid (Global)</div>
                <div className="grid grid-cols-2 gap-3 mb-3">
                    <div><label className="text-[10px] text-slate-500 uppercase font-semibold mb-1 block">Cell Width</label><input type="number" value={baseWidth} onChange={(e) => setBaseWidth(parseInt(e.target.value))} className="w-full bg-slate-950 border border-slate-700 rounded px-2 py-1.5 text-sm font-mono focus:border-indigo-500 focus:outline-none text-right"/></div>
                    <div><label className="text-[10px] text-slate-500 uppercase font-semibold mb-1 block">Cell Height</label><input type="number" value={baseHeight} onChange={(e) => setBaseHeight(parseInt(e.target.value))} className="w-full bg-slate-950 border border-slate-700 rounded px-2 py-1.5 text-sm font-mono focus:border-indigo-500 focus:outline-none text-right"/></div>
                </div>
                 {/* GAPS Controls */}
                 <div className="grid grid-cols-2 gap-3 mb-3">
                    <div><label className="text-[10px] text-slate-500 uppercase font-semibold mb-1 block flex items-center gap-1"><Ruler className="w-3 h-3"/> Gap X</label><input type="number" value={gapX} onChange={(e) => setGapX(parseInt(e.target.value))} className="w-full bg-slate-950 border border-slate-700 rounded px-2 py-1.5 text-sm font-mono focus:border-indigo-500 focus:outline-none text-right"/></div>
                    <div><label className="text-[10px] text-slate-500 uppercase font-semibold mb-1 block flex items-center gap-1"><Ruler className="w-3 h-3"/> Gap Y</label><input type="number" value={gapY} onChange={(e) => setGapY(parseInt(e.target.value))} className="w-full bg-slate-950 border border-slate-700 rounded px-2 py-1.5 text-sm font-mono focus:border-indigo-500 focus:outline-none text-right"/></div>
                </div>
                <div className="grid grid-cols-2 gap-3">
                     <div><label className="text-[10px] text-slate-500 uppercase font-semibold mb-1 block">Offset X</label><input type="number" value={globalOffsetX} onChange={(e) => setGlobalOffsetX(parseInt(e.target.value))} className="w-full bg-slate-950 border border-slate-700 rounded px-2 py-1.5 text-xs font-mono focus:border-pink-500 focus:outline-none text-right text-slate-400"/></div>
                     <div><label className="text-[10px] text-slate-500 uppercase font-semibold mb-1 block">Offset Y</label><input type="number" value={globalOffsetY} onChange={(e) => setGlobalOffsetY(parseInt(e.target.value))} className="w-full bg-slate-950 border border-slate-700 rounded px-2 py-1.5 text-xs font-mono focus:border-pink-500 focus:outline-none text-right text-slate-400"/></div>
                </div>
            </div>

            <div className="flex-1 flex flex-col min-h-0">
                 <div className="p-4 pb-2 flex items-center justify-between">
                    <div className="flex items-center gap-2 text-emerald-400 font-bold text-xs uppercase tracking-wider"><Layers className="w-3 h-3" /> Animation States</div>
                    <button onClick={addNewState} className="p-1 hover:bg-emerald-500/20 rounded text-emerald-400 transition"><Plus className="w-4 h-4" /></button>
                </div>
                <div className="flex-1 overflow-y-auto p-2 space-y-2">
                    {states.map(state => (
                        <div key={state.id} onClick={() => setActiveStateId(state.id)} className={`p-3 rounded-lg border cursor-pointer transition-all group relative ${activeStateId === state.id ? 'bg-slate-800 border-emerald-500 shadow-md' : 'bg-slate-900 border-slate-800 hover:border-slate-700'}`}>
                            <div className="flex justify-between items-start mb-2">
                                <input value={state.name} onChange={(e) => updateActiveState('name', e.target.value)} className={`bg-transparent font-bold text-sm w-full focus:outline-none ${activeStateId === state.id ? 'text-white' : 'text-slate-400'}`} onClick={(e) => e.stopPropagation()} />
                                <div className="flex items-center">
                                    <button onClick={(e) => { e.stopPropagation(); startAutoRecord(state.id); }} className={`p-1.5 transition rounded-md mr-1 ${autoRecordStateId === state.id ? 'bg-red-600 text-white animate-pulse' : 'text-slate-500 hover:text-blue-400 hover:bg-slate-700'}`} title="Download Video (Loop)"><Download className="w-3 h-3" /></button>
                                    <button onClick={(e) => { e.stopPropagation(); deleteState(state.id); }} className="opacity-0 group-hover:opacity-100 text-slate-500 hover:text-red-400 transition p-1"><Trash2 className="w-3 h-3" /></button>
                                </div>
                            </div>
                            {activeStateId === state.id && (
                                <div className="space-y-3 animate-in fade-in duration-200">
                                    <div className="bg-slate-950 rounded p-2 border border-slate-700">
                                        <div className="flex justify-between items-center mb-1">
                                            <span className="text-[10px] text-slate-500 uppercase font-bold">Sequence</span>
                                        </div>
                                        <input type="text" value={state.frames.join(', ')} onChange={(e) => handleSequenceChange(e.target.value)} className="w-full bg-slate-900 border border-slate-800 rounded px-2 py-1 text-xs font-mono text-emerald-300 focus:outline-none focus:border-emerald-500" placeholder="0, 1, 2..."/>
                                    </div>
                                    <div className="flex items-center gap-2">
                                        <div className="bg-slate-950 rounded p-1 flex items-center border border-slate-700 flex-1">
                                            <span className="text-[10px] text-slate-500 font-bold px-1">FPS</span>
                                            <input type="number" value={state.fps} onChange={(e) => updateActiveState('fps', parseInt(e.target.value))} className="w-full bg-transparent text-center text-xs focus:outline-none text-emerald-400"/>
                                        </div>
                                        {/* Flip Toggle */}
                                        <button 
                                            onClick={(e) => { e.stopPropagation(); updateActiveState('flipX', !state.flipX); }}
                                            className={`flex items-center justify-center px-2 rounded h-full border ${state.flipX ? 'bg-indigo-600 border-indigo-500 text-white' : 'bg-slate-950 border-slate-700 text-slate-500 hover:text-slate-300'}`}
                                            title="Mirror / Flip Horizontally"
                                        >
                                            <FlipHorizontal className="w-4 h-4" />
                                        </button>
                                    </div>
                                    
                                    {/* Custom Dimensions */}
                                    <div className="bg-slate-950/50 p-2 rounded border border-slate-700/50">
                                        <div className="flex justify-between mb-2">
                                            <label className="text-[10px] text-orange-400 font-bold uppercase flex items-center gap-1"><Ruler className="w-3 h-3" /> Custom Size (px)</label>
                                        </div>
                                        <div className="grid grid-cols-2 gap-2">
                                            <div>
                                                <label className="text-[9px] text-slate-500 block">Width</label>
                                                <input type="number" placeholder={baseWidth} value={state.customWidth || ''} onChange={(e) => updateActiveState('customWidth', e.target.value ? parseInt(e.target.value) : null)} className="w-full bg-slate-800 border border-slate-700 rounded px-2 py-1 text-xs text-orange-300 focus:outline-none"/>
                                            </div>
                                            <div>
                                                <label className="text-[9px] text-slate-500 block">Height</label>
                                                <input type="number" placeholder={baseHeight} value={state.customHeight || ''} onChange={(e) => updateActiveState('customHeight', e.target.value ? parseInt(e.target.value) : null)} className="w-full bg-slate-800 border border-slate-700 rounded px-2 py-1 text-xs text-orange-300 focus:outline-none"/>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            )}
                        </div>
                    ))}
                </div>
            </div>
        </aside>

        {/* Main Content Area */}
        <main className="flex-1 flex flex-col bg-slate-900 relative order-1 md:order-2 overflow-hidden">
            <div className="flex border-b border-slate-800 bg-slate-900 overflow-x-auto">
                <button onClick={() => setActiveTab('preview')} className={`px-6 py-3 text-sm font-medium whitespace-nowrap transition-colors ${activeTab === 'preview' ? 'text-white border-b-2 border-indigo-500 bg-slate-800' : 'text-slate-500 hover:text-slate-300'}`}>Visual Editor</button>
                <button onClick={() => setActiveTab('export')} className={`px-6 py-3 text-sm font-medium whitespace-nowrap transition-colors ${activeTab === 'export' ? 'text-white border-b-2 border-indigo-500 bg-slate-800' : 'text-slate-500 hover:text-slate-300'}`}>Get Code</button>
                <button onClick={() => setActiveTab('ai')} className={`px-6 py-3 text-sm font-medium whitespace-nowrap transition-colors flex items-center gap-2 ${activeTab === 'ai' ? 'text-purple-300 border-b-2 border-purple-500 bg-purple-900/10' : 'text-slate-500 hover:text-purple-300'}`}><Sparkles className="w-4 h-4" /> AI Lab</button>
            </div>

            <div className="flex-1 overflow-auto p-4 md:p-6 relative bg-slate-950/50">
                {activeTab === 'preview' && (
                    <div className="flex flex-col items-center h-full gap-6">
                        
                        {/* Preview Canvas Area */}
                        <div className="flex flex-col items-center gap-4 w-full max-w-md shrink-0">
                            <div className="bg-slate-900 p-2 rounded-xl shadow-2xl border border-slate-800 relative group w-full">
                                <div 
                                    className={`rounded-lg overflow-hidden relative flex items-center justify-center cursor-move w-full h-[240px] md:h-[300px]
                                    ${bgType === 'dark' ? "bg-[url('https://www.transparenttextures.com/patterns/dark-matter.png')] bg-slate-950" : 
                                      bgType === 'light' ? "bg-[url('https://www.transparenttextures.com/patterns/cubes.png')] bg-slate-200" : 
                                      "bg-green-500"}`}
                                >
                                    {/* Canvas */}
                                    <canvas 
                                        ref={canvasRef} 
                                        width={400} 
                                        height={300}
                                        onMouseDown={handleMouseDown}
                                        onMouseMove={handleMouseMove}
                                        onMouseUp={handleMouseUp}
                                        onMouseLeave={handleMouseUp}
                                        className="max-w-full max-h-full image-pixelated"
                                    />
                                    
                                    {/* Overlay Info */}
                                    <div className="absolute top-2 left-2 bg-black/50 backdrop-blur px-2 py-1 rounded text-[10px] text-slate-300 border border-white/10 pointer-events-none">
                                        State: <span className="text-white font-bold">{activeState.name}</span>
                                    </div>
                                    
                                    {autoRecordStateId && (
                                        <div className="absolute inset-0 flex items-center justify-center bg-black/50 z-40 pointer-events-none">
                                            <div className="bg-slate-900 px-4 py-2 rounded-full flex items-center gap-2 border border-red-500 text-white animate-pulse">
                                                <div className="w-3 h-3 bg-red-500 rounded-full"></div>
                                                <span className="text-xs font-bold">Recording...</span>
                                            </div>
                                        </div>
                                    )}

                                    {/* Background Controls Overlay */}
                                    <div className="absolute top-2 right-2 flex flex-col gap-1 opacity-0 group-hover:opacity-100 transition-opacity">
                                        <button onClick={() => setBgType('dark')} className="p-1 bg-slate-800 text-white rounded hover:bg-slate-700" title="Dark Mode"><Palette className="w-3 h-3"/></button>
                                        <button onClick={() => setBgType('light')} className="p-1 bg-slate-200 text-slate-800 rounded hover:bg-white" title="Light Mode"><Palette className="w-3 h-3"/></button>
                                        <button onClick={() => setBgType('green')} className="p-1 bg-green-500 text-white rounded hover:bg-green-400" title="Green Screen"><Video className="w-3 h-3"/></button>
                                        <button onClick={() => setPan({x:0, y:0})} className="p-1 bg-indigo-600 text-white rounded hover:bg-indigo-500 mt-2" title="Reset View"><Maximize2 className="w-3 h-3"/></button>
                                    </div>
                                </div>

                                {/* Canvas Controls */}
                                <div className="absolute -bottom-5 left-1/2 -translate-x-1/2 flex gap-2">
                                    <button onClick={() => setIsPlaying(!isPlaying)} disabled={!!autoRecordStateId} className={`px-4 py-1 rounded-full text-xs font-bold shadow-lg border flex items-center gap-1.5 transition-all ${isPlaying ? 'bg-slate-800 border-red-500/50 text-red-400' : 'bg-emerald-600 border-emerald-400 text-white'} ${autoRecordStateId ? 'opacity-50 cursor-not-allowed' : ''}`}>
                                        {isPlaying ? <><Pause className="w-3 h-3"/> Stop</> : <><Play className="w-3 h-3"/> Play</>}
                                    </button>
                                    <button onClick={() => setOnionSkin(!onionSkin)} disabled={!!autoRecordStateId} className={`px-4 py-1 rounded-full text-xs font-bold shadow-lg border flex items-center gap-1.5 transition-all ${onionSkin ? 'bg-blue-600 border-blue-400 text-white' : 'bg-slate-800 border-slate-700 text-slate-400'}`}>
                                        <Eye className="w-3 h-3"/> Ghost
                                    </button>
                                    <button onClick={toggleManualRecording} disabled={!!autoRecordStateId} className={`px-4 py-1 rounded-full text-xs font-bold shadow-lg border flex items-center gap-1.5 transition-all ${isRecording ? 'bg-red-600 border-red-400 text-white animate-pulse' : 'bg-slate-800 border-slate-700 text-slate-400 hover:text-white'}`}>
                                        <Video className="w-3 h-3"/> {isRecording ? 'Stop' : 'Rec'}
                                    </button>
                                </div>
                            </div>
                        </div>

                        {/* Sprite Map */}
                        <div className="w-full max-w-4xl bg-slate-900 rounded-xl border border-slate-800 shadow-lg flex flex-col overflow-hidden mt-2 flex-1 min-h-[200px]">
                            
                            {/* Map Header & Toolbar */}
                            <div className="px-4 py-2 bg-slate-800 border-b border-slate-700 flex flex-wrap gap-2 justify-between items-center">
                                <div className="flex items-center gap-4">
                                    <h3 className="text-xs font-bold text-slate-400 uppercase tracking-wider flex items-center gap-2"><ImageIcon className="w-3 h-3"/> Map</h3>
                                    <button 
                                        onClick={() => setShowGridTuner(!showGridTuner)}
                                        className={`px-2 py-1 rounded text-[10px] font-bold flex items-center gap-1 border transition ${showGridTuner ? 'bg-indigo-600 border-indigo-500 text-white' : 'bg-slate-700 border-slate-600 text-slate-400 hover:bg-slate-600'}`}
                                    >
                                        <SlidersHorizontal className="w-3 h-3" /> Tuner
                                    </button>
                                </div>
                                <div className="flex items-center gap-4">
                                    {(activeState.customWidth || activeState.customHeight) && (
                                        <label className="text-[10px] text-orange-400 flex items-center gap-2 cursor-pointer font-bold" title="Use custom state width/height for the mapping grid cells">
                                            <input type="checkbox" checked={syncGridToState} onChange={(e) => setSyncGridToState(e.target.checked)} className="rounded bg-slate-700 border-orange-500 accent-orange-500"/> 
                                            Sync Grid to State Size
                                        </label>
                                    )}
                                    <button 
                                        onClick={() => setIsMappingMode(!isMappingMode)}
                                        className={`px-3 py-1 rounded text-xs font-bold flex items-center gap-1 transition ${isMappingMode ? 'bg-emerald-600 text-white shadow-lg shadow-emerald-900/20' : 'bg-slate-700 text-slate-400 hover:bg-slate-600'}`}
                                    >
                                        <MousePointer2 className="w-3 h-3" /> {isMappingMode ? 'Mapping On' : 'Click to Map'}
                                    </button>
                                    <label className="text-xs text-slate-400 flex items-center gap-2 cursor-pointer">
                                        <input type="checkbox" checked={showGrid} onChange={(e) => setShowGrid(e.target.checked)} className="rounded bg-slate-700 border-slate-600 accent-indigo-500"/> Grid
                                    </label>
                                </div>
                            </div>

                            {/* Floating Grid Tuner (Overlay) */}
                            {showGridTuner && (
                                <div className="bg-slate-800 border-b border-slate-700 p-2 flex gap-4 items-center justify-center animate-in slide-in-from-top-2">
                                    <div className="flex gap-2 items-center">
                                        <span className="text-[10px] text-slate-500 uppercase font-bold">Grid W/H:</span>
                                        <input type="number" value={baseWidth} onChange={e => setBaseWidth(parseInt(e.target.value))} className="w-12 bg-slate-900 border border-slate-600 rounded text-center text-xs text-white"/>
                                        <input type="number" value={baseHeight} onChange={e => setBaseHeight(parseInt(e.target.value))} className="w-12 bg-slate-900 border border-slate-600 rounded text-center text-xs text-white"/>
                                    </div>
                                    <div className="w-[1px] h-4 bg-slate-600"></div>
                                    <div className="flex gap-2 items-center">
                                        <span className="text-[10px] text-slate-500 uppercase font-bold">Gap X/Y:</span>
                                        <input type="number" value={gapX} onChange={e => setGapX(parseInt(e.target.value))} className="w-10 bg-slate-900 border border-slate-600 rounded text-center text-xs text-white"/>
                                        <input type="number" value={gapY} onChange={e => setGapY(parseInt(e.target.value))} className="w-10 bg-slate-900 border border-slate-600 rounded text-center text-xs text-white"/>
                                    </div>
                                     <div className="w-[1px] h-4 bg-slate-600"></div>
                                    <div className="flex gap-2 items-center">
                                        <span className="text-[10px] text-slate-500 uppercase font-bold">Off X/Y:</span>
                                        <input type="number" value={globalOffsetX} onChange={e => setGlobalOffsetX(parseInt(e.target.value))} className="w-10 bg-slate-900 border border-slate-600 rounded text-center text-xs text-white"/>
                                        <input type="number" value={globalOffsetY} onChange={e => setGlobalOffsetY(parseInt(e.target.value))} className="w-10 bg-slate-900 border border-slate-600 rounded text-center text-xs text-white"/>
                                    </div>
                                </div>
                            )}

                            <div className="flex-1 overflow-auto p-4 bg-slate-950/50 flex justify-center relative">
                                <div className="relative inline-block shadow-2xl">
                                    <img src={imageSrc} alt="Reference" className="max-w-none opacity-60" style={{imageRendering: 'pixelated'}} />
                                    {showGrid && <GridOverlay />}
                                </div>
                            </div>
                        </div>
                    </div>
                )}

                {activeTab === 'export' && (
                    <div className="max-w-4xl mx-auto h-full flex flex-col">
                        <div className="bg-slate-900 rounded-xl border border-slate-800 overflow-hidden flex flex-col h-full shadow-2xl">
                            <div className="p-4 border-b border-slate-800 flex justify-between items-center bg-slate-900">
                                <div><h3 className="flex items-center gap-2 text-yellow-400 font-bold text-sm"><Code className="w-4 h-4" /> Generated Game Code</h3></div>
                                <button onClick={() => copyToClipboard(generateJS(), 'js')} className="flex items-center gap-2 px-4 py-2 bg-indigo-600 hover:bg-indigo-500 rounded-lg text-xs font-bold transition text-white shadow-lg">
                                    {copyFeedback === 'js' ? <Check className="w-4 h-4"/> : <Copy className="w-4 h-4"/>}{copyFeedback === 'js' ? 'Copied!' : 'Copy'}
                                </button>
                            </div>
                            <div className="flex-1 overflow-auto bg-[#0d1117] p-4"><pre className="text-xs font-mono text-yellow-100 whitespace-pre leading-relaxed">{generateJS()}</pre></div>
                        </div>
                    </div>
                )}

                {activeTab === 'ai' && (
                     <div className="max-w-5xl mx-auto h-full flex flex-col md:flex-row gap-6">
                        <div className="flex-1 flex flex-col gap-4">
                            <div className="bg-slate-900 rounded-xl border border-purple-500/30 overflow-hidden shadow-2xl flex-1 flex flex-col">
                                <div className="p-4 border-b border-purple-500/20 bg-gradient-to-r from-slate-900 to-purple-900/20"><h3 className="flex items-center gap-2 text-purple-300 font-bold text-sm"><Bot className="w-4 h-4" /> Insight</h3></div>
                                <div className="p-6 flex flex-col flex-1 items-center justify-center text-center gap-4">
                                     {!aiAnalysisResult ? (
                                         <div className="flex flex-col items-center gap-3">
                                             <p className="text-sm text-slate-400 max-w-xs">Send your current sprite sheet to Gemini Vision to identify themes, actions, and get name ideas.</p>
                                             <button onClick={handleAIAnalysis} disabled={isAnalyzing} className="mt-2 px-6 py-2 bg-purple-600 hover:bg-purple-500 text-white rounded-full font-bold text-sm flex items-center gap-2 transition disabled:opacity-50">{isAnalyzing ? <Loader className="w-4 h-4 animate-spin" /> : <Sparkles className="w-4 h-4" />} Analyze</button>
                                         </div>
                                     ) : (
                                         <div className="text-left w-full h-full overflow-auto p-2"><div className="prose prose-invert prose-sm max-w-none"><p className="whitespace-pre-line text-purple-100">{aiAnalysisResult}</p></div><button onClick={() => setAiAnalysisResult('')} className="mt-4 text-xs text-slate-500 hover:text-white underline">Clear</button></div>
                                     )}
                                </div>
                            </div>
                        </div>
                         <div className="flex-[1.5] flex flex-col gap-4">
                            <div className="bg-slate-900 rounded-xl border border-indigo-500/30 overflow-hidden shadow-2xl flex-1 flex flex-col">
                                <div className="p-4 border-b border-indigo-500/20 bg-gradient-to-r from-slate-900 to-indigo-900/20 flex justify-between items-center"><div><h3 className="flex items-center gap-2 text-indigo-300 font-bold text-sm"><Wand2 className="w-4 h-4" /> Exporter</h3></div></div>
                                <div className="p-4 bg-slate-950/30 border-b border-slate-800 flex flex-col md:flex-row gap-3">
                                    <select value={aiTargetEngine} onChange={(e) => setAiTargetEngine(e.target.value)} className="bg-slate-800 border border-slate-700 text-white text-sm rounded-lg focus:ring-indigo-500 focus:border-indigo-500 block w-full p-2.5">
                                        <option>Unity (C#)</option><option>Godot (GDScript)</option><option>Unreal Engine (C++)</option><option>Python (Pygame)</option><option>Roblox (Lua)</option><option>React (Three.js)</option>
                                    </select>
                                    <button onClick={handleAIExport} disabled={isGeneratingCode} className="px-4 py-2 bg-indigo-600 hover:bg-indigo-500 text-white rounded-lg font-bold text-sm whitespace-nowrap flex items-center gap-2 disabled:opacity-50">{isGeneratingCode ? <Loader className="w-4 h-4 animate-spin"/> : <Sparkles className="w-4 h-4"/> } Generate</button>
                                </div>
                                <div className="flex-1 overflow-auto bg-[#0d1117] p-4 relative min-h-[300px]">
                                    {aiCodeResult ? (
                                        <><button onClick={() => copyToClipboard(aiCodeResult, 'aiCode')} className="absolute top-4 right-4 p-2 bg-slate-800 rounded-md text-slate-400 hover:text-white hover:bg-slate-700 transition">{copyFeedback === 'aiCode' ? <Check className="w-4 h-4 text-green-400"/> : <Copy className="w-4 h-4"/>}</button><pre className="text-xs font-mono text-indigo-100 whitespace-pre-wrap">{aiCodeResult}</pre></>
                                    ) : (<div className="flex items-center justify-center h-full text-slate-600 text-sm italic">Select an engine and click generate...</div>)}
                                </div>
                            </div>
                        </div>
                     </div>
                )}
            </div>
        </main>
      </div>
    </div>
  );
};

export default SpriteAnimator;
