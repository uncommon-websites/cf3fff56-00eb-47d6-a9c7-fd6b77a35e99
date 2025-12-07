<script lang="ts">
	import { onMount } from 'svelte';

	// Icons
	const Icons = {
		Play: `<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="currentColor" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polygon points="5 3 19 12 5 21 5 3"></polygon></svg>`,
		ChevronDown: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m6 9 6 6 6-6"/></svg>`,
		ChevronRight: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m9 18 6-6-6-6"/></svg>`,
		ChevronLeft: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m15 18-6-6 6-6"/></svg>`,
		Text: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M17 6.1H3"/><path d="M21 12.1H3"/><path d="M15.1 18H3"/></svg>`,
		Music: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 18V5l12-2v13"/><circle cx="6" cy="18" r="3"/><circle cx="18" cy="16" r="3"/></svg>`,
		Wand: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 4V2"/><path d="M15 16v-2"/><path d="M8 9h2"/><path d="M20 9h2"/><path d="M17.8 11.8 19 13"/><path d="M15 9h0"/><path d="M17.8 6.2 19 5"/><path d="m3 21 9-9"/><path d="M12.2 6.2 11 5"/></svg>`,
		Captions: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect width="18" height="14" x="3" y="5" rx="2" ry="2"/><path d="M7 15h4M15 15h2M7 11h2M13 11h4"/></svg>`,
		Mic: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2a3 3 0 0 0-3 3v7a3 3 0 0 0 6 0V5a3 3 0 0 0-3-3Z"/><path d="M19 10v2a7 7 0 0 1-14 0v-2"/><line x1="12" x2="12" y1="19" y2="22"/></svg>`,
		FileText: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14.5 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V7.5L14.5 2z"/><polyline points="14 2 14 8 20 8"/></svg>`,
		Layers: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polygon points="12 2 2 7 12 12 22 7 12 2"/><polyline points="2 17 12 22 22 17"/><polyline points="2 12 12 17 22 12"/></svg>`,
		Video: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m22 8-6 4 6 4V8Z"/><rect width="14" height="12" x="2" y="6" rx="2" ry="2"/></svg>`,
		Plus: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14"/><path d="M12 5v14"/></svg>`,
		Check: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6 9 17l-5-5"/></svg>`,
		Globe: `<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><path d="M12 2a14.5 14.5 0 0 0 0 20 14.5 14.5 0 0 0 0-20"/><path d="M2 12h20"/></svg>`
	};

	const features = [
		{ title: 'Text & Audio Upload', icon: Icons.Text },
		{ title: 'Voice Cloning', icon: Icons.Mic },
		{ title: 'Multi-Channel Deploy', icon: Icons.Globe },
		{ title: 'Live Content Feeds', icon: Icons.Layers },
		{ title: 'Custom Behavior', icon: Icons.Wand },
		{ title: 'Privacy Controls', icon: Icons.FileText },
		{ title: 'Video Integration', icon: Icons.Video },
		{ title: 'Analytics Dashboard', icon: Icons.Captions, color: 'text-primary-500' }
	];

	const cloneExamples = [
		{ name: 'Brian Halligan', desc: "HubSpot co-founder sharing scaling insights", color: 'bg-primary-500' },
		{ name: 'Lennybot', desc: "Product expertise from Lenny Rachitsky", color: 'bg-primary-600' },
		{ name: 'Sam Feldt', desc: "Multi-platinum DJ for fan engagement", color: 'bg-secondary-500' },
		{ name: 'Vanessa Van Edwards', desc: "Behavioral research and communication", color: 'bg-primary-400' },
		{ name: 'Jay Shetty', desc: "Author and podcast host insights", color: 'bg-secondary-600' },
		{ name: 'Heather Monahan', desc: "Executive coaching and leadership", color: 'bg-primary-700' },
		{ name: 'Your Clone', desc: "Create your own digital mind", color: 'bg-gray-300' },
		{ name: 'Expert Clone', desc: "Share your unique knowledge at scale", color: 'bg-gray-400' },
	];

	const faqs = [
		"What is Delphi and how does it work?",
		"How does my AI clone learn my voice and style?",
		"What content can I upload to train my clone?",
		"Is my data private and secure?",
		"Can I deploy my clone on multiple platforms?",
		"How do I customize my clone's behavior?",
		"Can my clone speak multiple languages?",
		"What's the difference between Delphi tiers?",
		"How do I monetize my AI clone?",
		"Can I update my clone with new content?",
		"Who owns my digital mind and its responses?",
		"How accurate is the AI at capturing my knowledge?"
	];

    const footerLinks = {
        PRODUCT: ['AI Clone Platform', 'Voice & Style Training', 'Multi-Channel Deploy', 'Content Ingestion', 'Analytics', 'API Access', 'Mobile App', 'Delphi Immortal'],
        'USE CASES': ['For Experts', 'For Coaches', 'For Creators', 'For Business Owners', 'For Celebrities', 'For Writers', 'Lead Generation', 'Customer Support'],
        FEATURES: ['Text Upload', 'Audio & Video', 'Live Content Feeds', 'Voice Cloning', 'Custom Behavior', 'Privacy Controls', 'SMS & WhatsApp', 'Website Embed'],
        RESOURCES: ['API Documentation', 'Help Center', 'Case Studies', 'Blog', 'Community', 'Webinars', 'Clone Examples'],
        COMPANY: ['About Delphi', 'Careers', 'Privacy Policy', 'Terms of Service', 'Security', 'Contact Sales', 'Press Kit']
    };
</script>

<div class="min-h-screen bg-white font-sans text-gray-900">
	<!-- Navbar -->
	<nav class="sticky top-0 z-50 bg-white/80 backdrop-blur-md border-b border-gray-100">
		<div class="container-custom flex h-16 items-center justify-between">
			<div class="flex items-center gap-8">
				<a href="/" class="flex items-center gap-2 font-bold text-xl tracking-tight text-primary-600">
                    Delphi
                </a>
				<div class="hidden lg:flex items-center gap-6 text-sm font-medium text-gray-600">
					<a href="#" class="hover:text-primary-600 flex items-center gap-1">Product <span class="opacity-50 text-[10px]">▼</span></a>
					<a href="#" class="hover:text-primary-600 flex items-center gap-1">Use Cases <span class="opacity-50 text-[10px]">▼</span></a>
					<a href="#" class="hover:text-primary-600 flex items-center gap-1">API <span class="opacity-50 text-[10px]">▼</span></a>
					<a href="#" class="hover:text-primary-600 flex items-center gap-1">Resources <span class="opacity-50 text-[10px]">▼</span></a>
					<a href="#" class="hover:text-primary-600">Pricing</a>
					<a href="#" class="hover:text-primary-600">Clone Examples</a>
				</div>
			</div>
			<div class="flex items-center gap-4 text-sm font-medium">
				<a href="#" class="text-gray-600 hover:text-primary-600">Log in</a>
				<a href="#" class="bg-primary-600 text-white px-4 py-2 rounded-full hover:bg-primary-700 transition">Create Your Clone</a>
			</div>
		</div>
	</nav>

	<!-- Hero -->
	<section class="pt-20 pb-12">
		<div class="container-custom">
			<div class="flex flex-col lg:flex-row gap-12 mb-16">
				<div class="lg:w-1/2">
					<h1 class="text-5xl sm:text-6xl font-semibold tracking-tight leading-[1.1] mb-8">
						Never repeat yourself again
					</h1>
					<p class="text-xl text-gray-600 leading-relaxed mb-8 max-w-lg">
						Create an interactive AI clone that answers questions in your voice and style. Scale your knowledge without the repetitive effort.
					</p>
					<a href="#" class="inline-block bg-primary-600 text-white px-6 py-3 rounded-full font-medium hover:bg-primary-700 transition">
						Create Your Clone
					</a>
				</div>
				<div class="lg:w-1/2 lg:pt-2">
					<p class="text-lg text-gray-600 leading-relaxed max-w-lg mb-6">
						Built for experts, coaches, and creators who need to monetize knowledge but lack time for repetitive questions. Deploy your digital mind across SMS, WhatsApp, web, and voice.
					</p>
					<div class="flex flex-wrap gap-2">
						<div class="px-3 py-1 bg-primary-50 text-primary-700 rounded-full text-sm font-medium">Trusted by Brian Halligan</div>
						<div class="px-3 py-1 bg-primary-50 text-primary-700 rounded-full text-sm font-medium">Lennybot</div>
						<div class="px-3 py-1 bg-primary-50 text-primary-700 rounded-full text-sm font-medium">Sam Feldt</div>
					</div>
				</div>
			</div>

			<!-- Conversational Interface Mockup -->
			<div class="relative rounded-2xl overflow-hidden shadow-2xl border border-gray-200 bg-white aspect-[16/9] lg:aspect-[16/8]">
				<!-- Browser chrome/UI header -->
				<div class="absolute top-0 left-0 right-0 h-12 bg-gray-50 border-b border-gray-200 flex items-center justify-between px-4">
                    <div class="flex items-center gap-2">
                         <div class="w-3 h-3 rounded-full bg-red-400"></div>
                         <div class="w-3 h-3 rounded-full bg-yellow-400"></div>
                         <div class="w-3 h-3 rounded-full bg-green-400"></div>
                    </div>
                    <div class="text-xs font-medium text-gray-500">delphi.ai/brian-halligan</div>
                    <div class="w-16"></div>
                </div>
                
                <!-- Mockup Content -->
                <div class="absolute top-12 bottom-0 left-0 right-0 flex bg-gradient-to-br from-primary-50 to-white">
                    <!-- Main Conversation Area -->
                    <div class="flex-1 flex flex-col p-8">
                        <!-- Profile Header -->
                        <div class="flex items-center gap-4 mb-8">
                            <div class="w-16 h-16 rounded-full bg-gradient-to-br from-primary-400 to-primary-600"></div>
                            <div>
                                <h3 class="text-xl font-semibold text-gray-900">Brian Halligan</h3>
                                <p class="text-sm text-gray-600">HubSpot Co-founder • Sequoia Partner</p>
                            </div>
                        </div>
                        
                        <!-- Conversation -->
                        <div class="flex-1 space-y-4 overflow-hidden">
                            <!-- User Question -->
                            <div class="flex justify-end">
                                <div class="bg-primary-100 text-primary-900 px-4 py-3 rounded-2xl rounded-tr-sm max-w-md">
                                    <p class="text-sm">What's the most important lesson you learned scaling HubSpot from $0 to $30B?</p>
                                </div>
                            </div>
                            
                            <!-- AI Response -->
                            <div class="flex justify-start">
                                <div class="bg-white border border-gray-200 px-4 py-3 rounded-2xl rounded-tl-sm max-w-lg shadow-sm">
                                    <p class="text-sm text-gray-800 leading-relaxed">The biggest lesson was understanding that culture compounds. In the early days, we obsessed over our company values and hiring process. Every person you bring in either strengthens or dilutes your culture...</p>
                                    <div class="mt-2 flex items-center gap-2 text-xs text-gray-500">
                                        <div class="w-1.5 h-1.5 rounded-full bg-green-500"></div>
                                        <span>Answered instantly</span>
                                    </div>
                                </div>
                            </div>
                            
                            <!-- Suggested Questions -->
                            <div class="pt-4">
                                <p class="text-xs text-gray-500 mb-2">Suggested questions:</p>
                                <div class="flex flex-wrap gap-2">
                                    <button class="px-3 py-1.5 bg-white border border-gray-200 rounded-full text-xs hover:border-primary-300 transition">How did you approach fundraising?</button>
                                    <button class="px-3 py-1.5 bg-white border border-gray-200 rounded-full text-xs hover:border-primary-300 transition">What's your advice for first-time founders?</button>
                                </div>
                            </div>
                        </div>
                        
                        <!-- Input Area -->
                        <div class="mt-4 flex gap-2">
                            <input type="text" placeholder="Ask Brian anything..." class="flex-1 px-4 py-3 bg-white border border-gray-200 rounded-full text-sm focus:outline-none focus:border-primary-400" />
                            <button class="w-12 h-12 bg-primary-600 text-white rounded-full flex items-center justify-center hover:bg-primary-700 transition">
                                <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m22 2-7 20-4-9-9-4Z"/><path d="M22 2 11 13"/></svg>
                            </button>
                        </div>
                    </div>
                </div>
			</div>
            
            <div class="flex justify-center mt-6 gap-2">
                <button class="bg-white border border-gray-200 px-3 py-1 rounded-full text-xs font-medium shadow-sm flex items-center gap-1">
                    {@html Icons.Globe} Web
                </button>
                <button class="text-gray-400 px-3 py-1 rounded-full text-xs font-medium flex items-center gap-1">
                    {@html Icons.Mic} Voice
                </button>
                <button class="text-gray-400 px-3 py-1 rounded-full text-xs font-medium flex items-center gap-1">
                    {@html Icons.Text} SMS
                </button>
            </div>
		</div>
	</section>

	<!-- Intro Section -->
	<section class="py-20 bg-white">
		<div class="container-custom text-center">
			<p class="text-sm text-primary-600 font-medium mb-4">Conversational Media</p>
			<h2 class="text-4xl sm:text-5xl font-semibold tracking-tight max-w-4xl mx-auto mb-6 leading-[1.1]">
				The next evolution of knowledge transfer
			</h2>
			<p class="text-xl text-gray-600 max-w-3xl mx-auto mb-12 leading-relaxed">
				Delphi creates interactive AI clones that answer questions in your voice and style. Upload your content, train your digital mind, and deploy across every channel — from SMS to web to voice.
			</p>

			<div class="flex flex-wrap justify-center gap-3 mb-12 max-w-4xl mx-auto">
				{#each features as feature}
					<div class="flex items-center gap-2 px-3 py-1.5 bg-primary-50 rounded-full border border-primary-100 text-sm font-medium text-primary-700">
						<span class="{feature.color || 'text-primary-600'}">{@html feature.icon}</span>
						{feature.title}
					</div>
				{/each}
			</div>

			<button class="bg-primary-600 text-white px-6 py-3 rounded-full font-medium hover:bg-primary-700 transition flex items-center gap-2 mx-auto">
				<div class="w-5 h-5 fill-current">{@html Icons.Play}</div>
				See how it works
			</button>
		</div>
	</section>

	<!-- Feature Scroll Section -->
	<section class="py-20 border-t border-gray-100">
		<div class="container-custom">
			<div class="grid grid-cols-1 lg:grid-cols-2 gap-16">
				<!-- Left Column: Text -->
				<div class="space-y-32 py-12">
					<div class="max-w-md">
						<h3 class="text-3xl font-semibold mb-4">Upload your knowledge</h3>
						<p class="text-gray-600 leading-relaxed mb-6">
							Train your AI clone with text, audio, and video content. Link to live content feeds for continuous learning. Delphi indexes everything and mirrors your tone, style, and knowledge automatically.
						</p>
					</div>
                    
                    <div class="max-w-md">
						<h3 class="text-3xl font-semibold mb-4">Clone your voice and style</h3>
						<p class="text-gray-600 leading-relaxed mb-6">
							Your AI speaks only your words — no improvisation without consent. Customize behavior with notes on how your clone should respond. Built to protect your legacy and maintain authenticity over time.
						</p>
					</div>

                    <div class="max-w-md">
						<h3 class="text-3xl font-semibold mb-4">Deploy across every channel</h3>
						<p class="text-gray-600 leading-relaxed mb-6">
							Embed your clone on your website, deploy via SMS and WhatsApp, integrate with Slack, or enable voice and video interactions. One digital mind, unlimited touchpoints.
						</p>
					</div>

                    <div class="max-w-md">
						<h3 class="text-3xl font-semibold mb-4">Maintain relationships at scale</h3>
						<p class="text-gray-600 leading-relaxed mb-6">
							Never ghost anyone again. Your clone recognizes loyal fans, follows up with intent, and ensures the right people feel heard — while you focus on what matters most.
						</p>
					</div>

                    <div class="max-w-md">
						<h3 class="text-3xl font-semibold mb-4">Complete privacy and ownership</h3>
						<p class="text-gray-600 leading-relaxed mb-6">
							Strict privacy standards with encrypted storage. You own your digital mind completely. We never share or sell your data. Your knowledge, your control, your legacy.
						</p>
					</div>
				</div>

				<!-- Right Column: Sticky Visual -->
				<div class="relative hidden lg:block">
					<div class="sticky top-32 bg-gradient-to-br from-primary-50 to-white rounded-2xl border border-primary-100 p-6 h-[600px] overflow-hidden shadow-sm">
                        <div class="mb-4 text-xs font-medium text-primary-600 uppercase tracking-wider">Featured AI Clones</div>
                        <div class="space-y-2">
                            {#each cloneExamples as clone}
                                <div class="flex items-center gap-3 p-3 bg-white rounded-xl border border-gray-100 hover:border-primary-200 transition cursor-pointer group">
                                    <div class="w-10 h-10 rounded-full {clone.color} flex-shrink-0"></div>
                                    <div class="flex-1 min-w-0">
                                        <div class="font-medium text-sm text-gray-900 group-hover:text-primary-700">{clone.name}</div>
                                        <div class="text-xs text-gray-500 truncate">{clone.desc}</div>
                                    </div>
                                    <div class="w-6 h-6 rounded-full border border-primary-200 flex items-center justify-center text-primary-400 group-hover:bg-primary-50">
                                        <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg>
                                    </div>
                                </div>
                            {/each}
                        </div>
                        <!-- Fade out at bottom -->
                        <div class="absolute bottom-0 left-0 right-0 h-32 bg-gradient-to-t from-white to-transparent pointer-events-none"></div>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- Bento Grid Section -->
	<section class="py-20 bg-white">
		<div class="container-custom">
			<div class="text-center max-w-3xl mx-auto mb-16">
				<h2 class="text-4xl font-semibold mb-4">Everything you need to build and deploy your digital mind</h2>
				<p class="text-gray-600">
					From content ingestion to multi-channel deployment, Delphi combines every tool you need to create, customize, and scale your AI clone.
				</p>
			</div>

			<div class="grid grid-cols-1 md:grid-cols-3 gap-6">
				<!-- Content Ingestion (Span 2) -->
				<div class="md:col-span-2 bg-gradient-to-br from-primary-50 to-white rounded-2xl p-8 min-h-[300px] relative overflow-hidden group border border-primary-100">
                    <div class="relative z-10">
					    <h3 class="text-xl font-semibold mb-2">Content Ingestion</h3>
					    <p class="text-sm text-gray-600 max-w-xs">Upload text, audio, and video. Link to live content feeds for continuous learning. Your clone indexes everything automatically.</p>
                    </div>
                    <div class="absolute bottom-0 right-0 w-3/4 h-3/4 bg-white rounded-tl-2xl shadow-xl border border-gray-200 transform translate-y-4 translate-x-4 group-hover:translate-x-2 group-hover:translate-y-2 transition duration-500">
                         <!-- Mock content types -->
                         <div class="p-4 space-y-2">
                             <div class="flex items-center gap-2 h-8 bg-primary-100 rounded px-3">
                                 <span class="text-xs">📄</span>
                                 <span class="text-xs font-medium text-primary-700">Articles & Blog Posts</span>
                             </div>
                             <div class="flex items-center gap-2 h-8 bg-secondary-100 rounded px-3 ml-12">
                                 <span class="text-xs">🎙️</span>
                                 <span class="text-xs font-medium text-secondary-700">Podcast Episodes</span>
                             </div>
                             <div class="flex items-center gap-2 h-8 bg-primary-100 rounded px-3 ml-4">
                                 <span class="text-xs">🎥</span>
                                 <span class="text-xs font-medium text-primary-700">Video Content</span>
                             </div>
                         </div>
                    </div>
				</div>

				<!-- Multi-Channel Deploy -->
				<div class="bg-gradient-to-br from-primary-50 to-white rounded-2xl p-8 min-h-[300px] relative overflow-hidden border border-primary-100">
                    <div class="relative z-10">
					    <h3 class="text-xl font-semibold mb-2">Multi-Channel</h3>
					    <p class="text-sm text-gray-600">Deploy everywhere: SMS, WhatsApp, web, voice, video.</p>
                    </div>
                     <div class="absolute bottom-8 left-8 right-8 space-y-2">
                         <div class="bg-white rounded-lg p-2 shadow-sm border border-gray-200 flex items-center gap-2">
                             <div class="w-6 h-6 bg-green-500 rounded flex items-center justify-center text-white text-xs">💬</div>
                             <span class="text-xs font-medium">WhatsApp</span>
                         </div>
                         <div class="bg-white rounded-lg p-2 shadow-sm border border-gray-200 flex items-center gap-2">
                             <div class="w-6 h-6 bg-primary-500 rounded flex items-center justify-center text-white text-xs">🌐</div>
                             <span class="text-xs font-medium">Website</span>
                         </div>
                         <div class="bg-white rounded-lg p-2 shadow-sm border border-gray-200 flex items-center gap-2">
                             <div class="w-6 h-6 bg-blue-500 rounded flex items-center justify-center text-white text-xs">📱</div>
                             <span class="text-xs font-medium">SMS</span>
                         </div>
                     </div>
				</div>

				<!-- Privacy & Security -->
				<div class="bg-gradient-to-br from-primary-50 to-white rounded-2xl p-8 min-h-[300px] relative overflow-hidden border border-primary-100">
                    <div class="relative z-10">
					    <h3 class="text-xl font-semibold mb-2">Privacy First</h3>
					    <p class="text-sm text-gray-600">Encrypted storage. Complete ownership. Never shared or sold.</p>
                    </div>
                    <div class="absolute bottom-8 left-8 right-8 space-y-2">
                        <div class="flex items-center gap-2 text-xs">
                            <div class="w-4 h-4 bg-green-500 rounded-full flex items-center justify-center text-white">✓</div>
                            <span class="text-gray-700">End-to-end encryption</span>
                        </div>
                        <div class="flex items-center gap-2 text-xs">
                            <div class="w-4 h-4 bg-green-500 rounded-full flex items-center justify-center text-white">✓</div>
                            <span class="text-gray-700">You own your data</span>
                        </div>
                        <div class="flex items-center gap-2 text-xs">
                            <div class="w-4 h-4 bg-green-500 rounded-full flex items-center justify-center text-white">✓</div>
                            <span class="text-gray-700">No data sharing</span>
                        </div>
                    </div>
				</div>

				<!-- Analytics -->
				<div class="bg-gradient-to-br from-primary-50 to-white rounded-2xl p-8 min-h-[300px] relative overflow-hidden border border-primary-100">
                    <div class="relative z-10">
					    <h3 class="text-xl font-semibold mb-2">Signal Detection</h3>
					    <p class="text-sm text-gray-600">Reveal rising trends, hidden signals, and actionable moments.</p>
                    </div>
                    <div class="absolute bottom-8 left-8 right-8 bg-white rounded-xl p-3 shadow-sm border border-gray-200 text-xs space-y-2">
                        <div class="flex items-center justify-between">
                            <span class="font-medium text-gray-700">Top Question</span>
                            <span class="text-primary-600">↑ 45%</span>
                        </div>
                        <div class="text-gray-600 text-[10px]">"How do I get started with..."</div>
                         <div class="flex items-center justify-between mt-2">
                            <span class="font-medium text-gray-700">Engagement</span>
                            <span class="text-green-600">↑ 28%</span>
                        </div>
                        <div class="text-gray-600 text-[10px]">1,247 conversations this week</div>
                    </div>
				</div>

				<!-- Customization -->
				<div class="bg-gradient-to-br from-primary-50 to-white rounded-2xl p-8 min-h-[300px] relative overflow-hidden border border-primary-100">
                    <div class="relative z-10">
					    <h3 class="text-xl font-semibold mb-2">Custom Behavior</h3>
					    <p class="text-sm text-gray-600">Fine-tune how your clone responds with customization notes.</p>
                    </div>
                    <div class="absolute bottom-8 left-8 right-8 bg-white rounded-xl shadow-sm border border-gray-200 overflow-hidden">
                        <div class="p-2 border-b border-gray-100 text-xs">
                            <span class="font-medium text-gray-700">Tone:</span> <span class="text-gray-600">Professional yet approachable</span>
                        </div>
                        <div class="p-2 border-b border-gray-100 text-xs">
                            <span class="font-medium text-gray-700">Style:</span> <span class="text-gray-600">Concise, actionable advice</span>
                        </div>
                         <div class="p-2 text-xs">
                            <span class="font-medium text-gray-700">Focus:</span> <span class="text-gray-600">Scaling strategies</span>
                        </div>
                    </div>
				</div>
			</div>
		</div>
	</section>

	<!-- Use Cases Section -->
	<section class="py-20">
		<div class="container-custom">
			<div class="text-center max-w-3xl mx-auto mb-16">
				<h2 class="text-4xl font-semibold mb-4">Built for experts who scale knowledge</h2>
				<p class="text-gray-600">
					From thought leaders to coaches and creators, Delphi helps you monetize expertise, maintain relationships, and capture every opportunity — without burning out.
				</p>
			</div>

			<div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <!-- Card 1 -->
                <div class="group cursor-pointer">
                    <div class="aspect-square rounded-2xl overflow-hidden mb-4 relative">
                        <img src="/generated/image-a-professional-coach-reviewing-questions-1765127010789-1.webp" alt="Coaches" class="w-full h-full object-cover transition duration-500 group-hover:scale-105" />
                        <div class="absolute inset-0 bg-gradient-to-t from-primary-900/60 to-transparent"></div>
                        <div class="absolute bottom-4 left-4 right-4">
                            <div class="text-white text-sm font-medium">For Coaches</div>
                        </div>
                    </div>
                    <h3 class="text-lg font-semibold mb-2">Coaches & Consultants</h3>
                    <p class="text-sm text-gray-600 leading-relaxed">Answer unlimited client questions, create personalized learning experiences, and maintain relationships at scale without sacrificing quality or time.</p>
                </div>

                 <!-- Card 2 -->
                <div class="group cursor-pointer">
                    <div class="aspect-square rounded-2xl overflow-hidden mb-4 relative">
                        <img src="/generated/image-a-business-owner-in-casual-attire-having-1765127016332-2.webp" alt="Business Owners" class="w-full h-full object-cover transition duration-500 group-hover:scale-105" />
                         <div class="absolute inset-0 bg-gradient-to-t from-primary-900/60 to-transparent"></div>
                         <div class="absolute bottom-4 left-4 right-4">
                            <div class="text-white text-sm font-medium">For Business</div>
                        </div>
                    </div>
                    <h3 class="text-lg font-semibold mb-2">Business Owners</h3>
                    <p class="text-sm text-gray-600 leading-relaxed">Turn every website visit into a conversation. Capture leads, share products, and provide instant support while you focus on building your business.</p>
                </div>

                 <!-- Card 3 -->
                <div class="group cursor-pointer">
                    <div class="aspect-square rounded-2xl overflow-hidden mb-4 relative">
                        <img src="/generated/image-a-content-creator-recording-themselves-s-1765127021019-3.webp" alt="Creators" class="w-full h-full object-cover transition duration-500 group-hover:scale-105" />
                         <div class="absolute inset-0 bg-gradient-to-t from-primary-900/60 to-transparent"></div>
                         <div class="absolute bottom-4 left-4 right-4">
                            <div class="text-white text-sm font-medium">For Creators</div>
                        </div>
                    </div>
                    <h3 class="text-lg font-semibold mb-2">Creators & Influencers</h3>
                    <p class="text-sm text-gray-600 leading-relaxed">Build deeper audience connections, monetize your knowledge, and never ghost your fans. Your clone ensures everyone feels heard.</p>
                </div>
            </div>
		</div>
	</section>

	<!-- API Section -->
	<section class="py-20 bg-gradient-to-br from-primary-50 to-white">
		<div class="container-custom">
			<div class="text-center max-w-3xl mx-auto mb-16">
				<h2 class="text-4xl font-semibold mb-4">Integrate your AI clone anywhere with our API</h2>
				<p class="text-gray-600">
					Embed conversational AI into your app, website, or workflow. Access the same technology powering thousands of digital minds — programmatically, at scale.
				</p>
			</div>

			<div class="max-w-3xl mx-auto bg-white rounded-xl shadow-sm border border-primary-200 p-6 overflow-x-auto">
				<pre class="text-sm font-mono leading-relaxed text-gray-800">
<span class="text-primary-600">import</span> &#123; DelphiClient &#125; <span class="text-primary-600">from</span> <span class="text-green-600">"@delphi/sdk"</span>;

<span class="text-primary-600">const</span> delphi = <span class="text-primary-600">new</span> <span class="text-secondary-600">DelphiClient</span>(&#123; 
  apiKey: <span class="text-green-600">"YOUR_API_KEY"</span> 
&#125;);

<span class="text-primary-600">const</span> response = <span class="text-primary-600">await</span> delphi.clone.<span class="text-blue-600">ask</span>(&#123;
  cloneId: <span class="text-green-600">"brian-halligan"</span>,
  question: <span class="text-green-600">"What's your advice for scaling a startup?"</span>,
  context: &#123; 
    channel: <span class="text-green-600">"web"</span>,
    userId: <span class="text-green-600">"user_123"</span> 
  &#125;
&#125;);

console.<span class="text-blue-600">log</span>(response.answer);
<span class="text-gray-500">// "The biggest lesson was understanding that culture compounds..."</span></pre>
			</div>
			
			<div class="text-center mt-8">
				<a href="#" class="text-primary-600 font-medium hover:text-primary-700">View API Documentation →</a>
			</div>
		</div>
	</section>

	<!-- FAQ Section -->
	<section class="py-20">
		<div class="container-custom">
			<h2 class="text-4xl font-semibold mb-12">Frequently asked questions</h2>
			<div class="border-t border-gray-200">
				{#each faqs as faq}
					<details class="group border-b border-gray-200">
						<summary class="flex items-center justify-between py-6 cursor-pointer list-none hover:text-primary-600 transition">
							<span class="text-lg font-medium">{faq}</span>
							<span class="transform group-open:rotate-45 transition-transform duration-200 text-primary-600">
								{@html Icons.Plus}
							</span>
						</summary>
						<div class="pb-6 text-gray-600 leading-relaxed max-w-3xl">
							<p>Delphi creates interactive AI clones that capture your voice, style, and knowledge. Upload your content, customize behavior, and deploy across multiple channels to scale your expertise without repetitive effort.</p>
						</div>
					</details>
				{/each}
			</div>
		</div>
	</section>

	<!-- Bottom CTA -->
	<section class="py-24 bg-gradient-to-br from-primary-600 to-primary-700 text-white">
		<div class="container-custom flex flex-col md:flex-row items-center justify-between gap-8">
			<div>
				<h2 class="text-4xl font-semibold mb-2">Ready to clone yourself?</h2>
				<p class="text-primary-100 text-lg">Join thousands of experts scaling their knowledge with AI</p>
			</div>
			<div class="flex items-center gap-4">
				<a href="#" class="bg-white text-primary-600 px-6 py-3 rounded-full font-medium hover:bg-primary-50 transition">
					Create Your Clone
				</a>
				<a href="#" class="bg-primary-700 border border-primary-500 text-white px-6 py-3 rounded-full font-medium hover:bg-primary-800 transition">
					Talk to sales
				</a>
			</div>
		</div>
	</section>

	<!-- Footer -->
	<footer class="bg-white pt-20 pb-10 border-t border-gray-100 text-xs">
		<div class="container-custom">
			<div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-8 mb-20">
                {#each Object.entries(footerLinks) as [category, links]}
                    <div>
                        <h4 class="font-bold text-gray-400 mb-6 tracking-wider">{category}</h4>
                        <ul class="space-y-3">
                            {#each links as link}
                                <li><a href="#" class="text-gray-600 hover:text-primary-600 transition">{link}</a></li>
                            {/each}
                        </ul>
                    </div>
                {/each}
			</div>

			<div class="flex flex-col md:flex-row items-center justify-between pt-8 border-t border-gray-100 gap-4">
				<div class="flex items-center gap-2 font-bold text-xl tracking-tight text-primary-600">
                    Delphi
                </div>
                
                <div class="flex flex-wrap justify-center gap-6 text-gray-500">
                    <a href="#" class="hover:text-primary-600">Privacy Policy</a>
                    <a href="#" class="hover:text-primary-600">Terms of Service</a>
                    <a href="#" class="hover:text-primary-600">Security</a>
                    <a href="#" class="hover:text-primary-600">© 2024 Delphi</a>
                </div>

                 <div class="flex items-center gap-2 text-gray-500">
                    <div class="w-2 h-2 rounded-full bg-green-500"></div>
                    <span>All systems operational</span>
                </div>
			</div>
		</div>
	</footer>
</div>

<style>
    /* Custom scrollbar for code block */
    pre::-webkit-scrollbar {
        height: 8px;
    }
    pre::-webkit-scrollbar-track {
        background: transparent;
    }
    pre::-webkit-scrollbar-thumb {
        background-color: #e5e7eb;
        border-radius: 4px;
    }
</style>

