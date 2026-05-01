import { useState, useRef, useEffect } from "react";

const SUGGESTIONS = [
  "বাংলাদেশের সেরা পর্যটন স্থান কোনগুলো?",
  "আজকের আবহাওয়া কেমন?",
  "AI কীভাবে কাজ করে?",
  "ক্রিপ্টোকারেন্সি কি নিরাপদ বিনিয়োগ?",
];

function SourceCard({ url, index }) {
  let domain = "";
  try {
    domain = new URL(url).hostname.replace("www.", "");
  } catch {
    domain = url.slice(0, 30);
  }
  return (
    <a
      href={url}
      target="_blank"
      rel="noopener noreferrer"
      style={{
        display: "flex",
        alignItems: "center",
        gap: "8px",
        background: "rgba(255,255,255,0.04)",
        border: "1px solid rgba(255,255,255,0.08)",
        borderRadius: "10px",
        padding: "8px 12px",
        textDecoration: "none",
        color: "#a0b4d0",
        fontSize: "12px",
        transition: "all 0.2s",
        minWidth: 0,
        flexShrink: 0,
      }}
      onMouseEnter={e => {
        e.currentTarget.style.background = "rgba(99,179,237,0.1)";
        e.currentTarget.style.borderColor = "rgba(99,179,237,0.3)";
        e.currentTarget.style.color = "#63b3ed";
      }}
      onMouseLeave={e => {
        e.currentTarget.style.background = "rgba(255,255,255,0.04)";
        e.currentTarget.style.borderColor = "rgba(255,255,255,0.08)";
        e.currentTarget.style.color = "#a0b4d0";
      }}
    >
      <span style={{
        background: "rgba(99,179,237,0.15)",
        color: "#63b3ed",
        borderRadius: "50%",
        width: "18px",
        height: "18px",
        display: "flex",
        alignItems: "center",
        justifyContent: "center",
        fontSize: "10px",
        fontWeight: "bold",
        flexShrink: 0,
      }}>{index + 1}</span>
      <span style={{ overflow: "hidden", textOverflow: "ellipsis", whiteSpace: "nowrap" }}>{domain}</span>
    </a>
  );
}

function TypewriterText({ text }) {
  const [displayed, setDisplayed] = useState("");
  const idx = useRef(0);
  useEffect(() => {
    setDisplayed("");
    idx.current = 0;
    if (!text) return;
    const interval = setInterval(() => {
      if (idx.current < text.length) {
        setDisplayed(text.slice(0, idx.current + 1));
        idx.current++;
      } else {
        clearInterval(interval);
      }
    }, 8);
    return () => clearInterval(interval);
  }, [text]);
  return <span>{displayed}</span>;
}

function ThinkingDots() {
  return (
    <div style={{ display: "flex", gap: "6px", alignItems: "center", padding: "8px 0" }}>
      {[0, 1, 2].map(i => (
        <div key={i} style={{
          width: "8px", height: "8px",
          borderRadius: "50%",
          background: "#63b3ed",
          animation: "pulse 1.2s ease-in-out infinite",
          animationDelay: `${i * 0.2}s`,
          opacity: 0.7,
        }} />
      ))}
    </div>
  );
}

export default function AISearch() {
  const [query, setQuery] = useState("");
  const [history, setHistory] = useState([]);
  const [loading, setLoading] = useState(false);
  const [focused, setFocused] = useState(false);
  const inputRef = useRef(null);
  const bottomRef = useRef(null);

  useEffect(() => {
    if (bottomRef.current) {
      bottomRef.current.scrollIntoView({ behavior: "smooth" });
    }
  }, [history, loading]);

  const search = async (q) => {
    if (!q.trim() || loading) return;
    const userMsg = q.trim();
    setQuery("");
    setLoading(true);

    setHistory(prev => [...prev, { role: "user", content: userMsg }, { role: "assistant", content: null, sources: [], loading: true }]);

    try {
      const response = await fetch("https://api.anthropic.com/v1/messages", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          model: "claude-sonnet-4-20250514",
          max_tokens: 1000,
          system: `তুমি একটি স্মার্ট AI সার্চ অ্যাসিস্ট্যান্ট। ওয়েব সার্চ করে সবচেয়ে আপডেট এবং সঠিক তথ্য দাও। উত্তর বাংলায় দাও যদি প্রশ্ন বাংলায় হয়, ইংরেজিতে হলে ইংরেজিতে দাও। উত্তর সংক্ষিপ্ত, তথ্যপূর্ণ এবং মানসম্পন্ন হওয়া চাই। মার্কডাউন ব্যবহার করতে পারো।`,
          messages: [{ role: "user", content: userMsg }],
          tools: [{ type: "web_search_20250305", name: "web_search" }],
        }),
      });

      const data = await response.json();

      let answerText = "";
      let sources = [];

      for (const block of data.content || []) {
        if (block.type === "text") answerText += block.text;
        if (block.type === "tool_result" || block.type === "mcp_tool_result") {
          try {
            const parsed = JSON.parse(block.content?.[0]?.text || "{}");
            if (parsed.results) {
              sources = parsed.results.map(r => r.url).filter(Boolean);
            }
          } catch {}
        }
      }

      // Extract citations from text if any
      const urlRegex = /https?:\/\/[^\s\)\"]+/g;
      const found = answerText.match(urlRegex) || [];
      const allSources = [...new Set([...sources, ...found])].slice(0, 6);

      setHistory(prev => {
        const next = [...prev];
        const lastIdx = next.length - 1;
        next[lastIdx] = { role: "assistant", content: answerText || "কোনো উত্তর পাওয়া যায়নি।", sources: allSources, loading: false };
        return next;
      });
    } catch (err) {
      setHistory(prev => {
        const next = [...prev];
        const lastIdx = next.length - 1;
        next[lastIdx] = { role: "assistant", content: "❌ সার্ভারে সমস্যা হয়েছে। আবার চেষ্টা করুন।", sources: [], loading: false };
        return next;
      });
    }

    setLoading(false);
  };

  const handleKey = (e) => {
    if (e.key === "Enter" && !e.shiftKey) {
      e.preventDefault();
      search(query);
    }
  };

  const isEmpty = history.length === 0;

  return (
    <div style={{
      minHeight: "100vh",
      background: "#0a0f1a",
      color: "#e2e8f0",
      fontFamily: "'Georgia', 'Times New Roman', serif",
      display: "flex",
      flexDirection: "column",
      alignItems: "center",
    }}>
      <style>{`
        @keyframes pulse {
          0%, 100% { transform: scale(1); opacity: 0.5; }
          50% { transform: scale(1.3); opacity: 1; }
        }
        @keyframes fadeIn {
          from { opacity: 0; transform: translateY(12px); }
          to { opacity: 1; transform: translateY(0); }
        }
        @keyframes shimmer {
          0% { background-position: -200% 0; }
          100% { background-position: 200% 0; }
        }
        * { box-sizing: border-box; }
        ::-webkit-scrollbar { width: 4px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: rgba(99,179,237,0.3); border-radius: 2px; }
        textarea { resize: none; }
      `}</style>

      {/* Header */}
      <div style={{
        width: "100%",
        maxWidth: "720px",
        padding: "24px 20px 0",
        display: "flex",
        alignItems: "center",
        justifyContent: isEmpty ? "center" : "flex-start",
        transition: "all 0.4s ease",
      }}>
        <div style={{ display: "flex", alignItems: "center", gap: "10px" }}>
          <div style={{
            width: "36px", height: "36px",
            background: "linear-gradient(135deg, #63b3ed, #4299e1)",
            borderRadius: "10px",
            display: "flex", alignItems: "center", justifyContent: "center",
            fontSize: "18px",
            boxShadow: "0 0 20px rgba(99,179,237,0.4)",
          }}>🔍</div>
          <span style={{
            fontSize: "20px",
            fontWeight: "bold",
            background: "linear-gradient(90deg, #63b3ed, #a78bfa)",
            WebkitBackgroundClip: "text",
            WebkitTextFillColor: "transparent",
            letterSpacing: "-0.5px",
          }}>AiSearch</span>
        </div>
      </div>

      {/* Main */}
      <div style={{
        flex: 1,
        width: "100%",
        maxWidth: "720px",
        padding: "0 20px",
        display: "flex",
        flexDirection: "column",
      }}>
        {/* Hero */}
        {isEmpty && (
          <div style={{
            display: "flex",
            flexDirection: "column",
            alignItems: "center",
            justifyContent: "center",
            flex: 1,
            paddingTop: "80px",
            animation: "fadeIn 0.5s ease",
          }}>
            <h1 style={{
              fontSize: "clamp(28px, 5vw, 44px)",
              fontWeight: "bold",
              textAlign: "center",
              marginBottom: "12px",
              lineHeight: 1.2,
              background: "linear-gradient(135deg, #e2e8f0 0%, #63b3ed 50%, #a78bfa 100%)",
              WebkitBackgroundClip: "text",
              WebkitTextFillColor: "transparent",
            }}>
              যা জানতে চাও, জিজ্ঞেস করো
            </h1>
            <p style={{ color: "#718096", fontSize: "16px", marginBottom: "48px", textAlign: "center" }}>
              Real-time web search • AI-powered answers
            </p>

            <div style={{ display: "flex", flexWrap: "wrap", gap: "10px", justifyContent: "center", marginBottom: "40px" }}>
              {SUGGESTIONS.map((s, i) => (
                <button key={i} onClick={() => search(s)} style={{
                  background: "rgba(255,255,255,0.04)",
                  border: "1px solid rgba(255,255,255,0.1)",
                  borderRadius: "20px",
                  padding: "8px 16px",
                  color: "#a0aec0",
                  fontSize: "13px",
                  cursor: "pointer",
                  transition: "all 0.2s",
                  fontFamily: "inherit",
                }}
                onMouseEnter={e => {
                  e.currentTarget.style.background = "rgba(99,179,237,0.1)";
                  e.currentTarget.style.borderColor = "rgba(99,179,237,0.3)";
                  e.currentTarget.style.color = "#63b3ed";
                }}
                onMouseLeave={e => {
                  e.currentTarget.style.background = "rgba(255,255,255,0.04)";
                  e.currentTarget.style.borderColor = "rgba(255,255,255,0.1)";
                  e.currentTarget.style.color = "#a0aec0";
                }}>
                  {s}
                </button>
              ))}
            </div>
          </div>
        )}

        {/* Conversation */}
        {!isEmpty && (
          <div style={{ flex: 1, paddingTop: "32px", paddingBottom: "20px" }}>
            {history.map((msg, i) => (
              <div key={i} style={{ animation: "fadeIn 0.4s ease", marginBottom: "32px" }}>
                {msg.role === "user" ? (
                  <div style={{ display: "flex", justifyContent: "flex-end" }}>
                    <div style={{
                      background: "linear-gradient(135deg, #2d3748, #1a202c)",
                      border: "1px solid rgba(255,255,255,0.1)",
                      borderRadius: "16px 16px 4px 16px",
                      padding: "12px 18px",
                      maxWidth: "85%",
                      fontSize: "15px",
                      lineHeight: 1.6,
                      color: "#e2e8f0",
                    }}>
                      {msg.content}
                    </div>
                  </div>
                ) : (
                  <div>
                    <div style={{ display: "flex", alignItems: "center", gap: "8px", marginBottom: "12px" }}>
                      <div style={{
                        width: "24px", height: "24px",
                        background: "linear-gradient(135deg, #63b3ed, #4299e1)",
                        borderRadius: "6px",
                        display: "flex", alignItems: "center", justifyContent: "center",
                        fontSize: "12px",
                        boxShadow: "0 0 10px rgba(99,179,237,0.3)",
                      }}>✦</div>
                      <span style={{ color: "#63b3ed", fontSize: "13px", fontWeight: "bold", letterSpacing: "0.5px" }}>AiSearch</span>
                    </div>

                    {msg.loading ? (
                      <ThinkingDots />
                    ) : (
                      <>
                        {msg.sources && msg.sources.length > 0 && (
                          <div style={{ marginBottom: "16px" }}>
                            <div style={{ color: "#718096", fontSize: "11px", marginBottom: "8px", letterSpacing: "1px", textTransform: "uppercase" }}>সূত্র</div>
                            <div style={{ display: "flex", gap: "8px", flexWrap: "wrap" }}>
                              {msg.sources.slice(0, 5).map((url, si) => (
                                <SourceCard key={si} url={url} index={si} />
                              ))}
                            </div>
                          </div>
                        )}
                        <div style={{
                          fontSize: "15px",
                          lineHeight: 1.8,
                          color: "#cbd5e0",
                          whiteSpace: "pre-wrap",
                        }}>
                          {i === history.length - 1 ? <TypewriterText text={msg.content} /> : msg.content}
                        </div>
                      </>
                    )}
                  </div>
                )}
              </div>
            ))}
            <div ref={bottomRef} />
          </div>
        )}
      </div>

      {/* Input */}
      <div style={{
        width: "100%",
        maxWidth: "720px",
        padding: "16px 20px 28px",
        position: "sticky",
        bottom: 0,
        background: "linear-gradient(to top, #0a0f1a 80%, transparent)",
      }}>
        <div style={{
          display: "flex",
          alignItems: "flex-end",
          gap: "10px",
          background: "rgba(255,255,255,0.05)",
          border: `1px solid ${focused ? "rgba(99,179,237,0.5)" : "rgba(255,255,255,0.1)"}`,
          borderRadius: "16px",
          padding: "12px 14px",
          transition: "border-color 0.2s",
          boxShadow: focused ? "0 0 0 3px rgba(99,179,237,0.1)" : "none",
        }}>
          <textarea
            ref={inputRef}
            value={query}
            onChange={e => setQuery(e.target.value)}
            onKeyDown={handleKey}
            onFocus={() => setFocused(true)}
            onBlur={() => setFocused(false)}
            placeholder="যেকোনো প্রশ্ন করো..."
            rows={1}
            style={{
              flex: 1,
              background: "transparent",
              border: "none",
              outline: "none",
              color: "#e2e8f0",
              fontSize: "15px",
              fontFamily: "inherit",
              lineHeight: 1.6,
              maxHeight: "120px",
              overflow: "auto",
            }}
            onInput={e => {
              e.target.style.height = "auto";
              e.target.style.height = Math.min(e.target.scrollHeight, 120) + "px";
            }}
          />
          <button
            onClick={() => search(query)}
            disabled={loading || !query.trim()}
            style={{
              width: "36px",
              height: "36px",
              borderRadius: "10px",
              border: "none",
              background: loading || !query.trim() ? "rgba(99,179,237,0.2)" : "linear-gradient(135deg, #63b3ed, #4299e1)",
              color: loading || !query.trim() ? "#4a5568" : "#fff",
              cursor: loading || !query.trim() ? "not-allowed" : "pointer",
              display: "flex",
              alignItems: "center",
              justifyContent: "center",
              fontSize: "16px",
              flexShrink: 0,
              transition: "all 0.2s",
              boxShadow: loading || !query.trim() ? "none" : "0 0 16px rgba(99,179,237,0.4)",
            }}
          >
            {loading ? "⏳" : "↑"}
          </button>
        </div>
        <div style={{ textAlign: "center", marginTop: "10px", color: "#4a5568", fontSize: "11px" }}>
          Claude AI • Real-time Web Search
        </div>
      </div>
    </div>
  );
}
