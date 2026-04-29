<script lang="ts">
	import { onMount } from 'svelte';
	import {
		personalInfo,
		objective,
		education,
		experience,
		activities,
		projects,
		skills,
		certificates,
		hobbies,
		additionalInfo
	} from '$lib/data';
	import Section from '$lib/components/Section.svelte';
	import TimelineItem from '$lib/components/TimelineItem.svelte';
	import SkillBar from '$lib/components/SkillBar.svelte';
	import ProjectCard from '$lib/components/ProjectCard.svelte';
	import { Sun, Moon, Monitor } from 'lucide-svelte';

	import AOS from 'aos';
	import 'aos/dist/aos.css';

	type Theme = 'light' | 'dark' | 'system';
	let theme = $state<Theme>('system');

	function applyTheme(t: Theme) {
		if (typeof window === 'undefined') return;
		
		const root = window.document.documentElement;
		root.classList.remove('light', 'dark');

		if (t === 'system') {
			const systemTheme = window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';
			root.classList.add(systemTheme);
		} else {
			root.classList.add(t);
		}
		
		localStorage.setItem('theme', t);
		theme = t;
	}

	onMount(() => {
		const savedTheme = localStorage.getItem('theme') as Theme | null;
		if (savedTheme) {
			applyTheme(savedTheme);
		} else {
			applyTheme('system');
		}

		AOS.init({
			duration: 1000,
			once: true,
			offset: 100,
			easing: 'ease-in-out'
		});

		const mediaQuery = window.matchMedia('(prefers-color-scheme: dark)');
		const handleChange = () => {
			if (theme === 'system') applyTheme('system');
		};
		mediaQuery.addEventListener('change', handleChange);
		return () => mediaQuery.removeEventListener('change', handleChange);
	});
</script>

<svelte:head>
	<title>{personalInfo.name} - {personalInfo.title}</title>
</svelte:head>

<main class="min-h-screen bg-gray-50 dark:bg-gray-950 transition-colors duration-300 py-10 px-4 sm:px-6 lg:px-8">
	<!-- Theme Toggle -->
	<div class="fixed top-4 right-4 z-50 flex bg-white dark:bg-gray-800 shadow-lg rounded-full p-1 border border-gray-200 dark:border-gray-700">
		<button 
			onclick={() => applyTheme('light')}
			class="p-2 rounded-full transition-all {theme === 'light' ? 'bg-blue-100 text-blue-600 dark:bg-blue-900 dark:text-blue-300' : 'text-gray-500 hover:bg-gray-100 dark:hover:bg-gray-700'}"
			title="Light Mode"
		>
			<Sun size={20} />
		</button>
		<button 
			onclick={() => applyTheme('dark')}
			class="p-2 rounded-full transition-all {theme === 'dark' ? 'bg-blue-100 text-blue-600 dark:bg-blue-900 dark:text-blue-300' : 'text-gray-500 hover:bg-gray-100 dark:hover:bg-gray-700'}"
			title="Dark Mode"
		>
			<Moon size={20} />
		</button>
		<button 
			onclick={() => applyTheme('system')}
			class="p-2 rounded-full transition-all {theme === 'system' ? 'bg-blue-100 text-blue-600 dark:bg-blue-900 dark:text-blue-300' : 'text-gray-500 hover:bg-gray-100 dark:hover:bg-gray-700'}"
			title="System Theme"
		>
			<Monitor size={20} />
		</button>
	</div>

	<div class="max-w-5xl mx-auto bg-white dark:bg-gray-900 shadow-xl rounded-2xl overflow-hidden transition-colors duration-300" data-aos="fade-up">
		<!-- Header -->
		<header class="bg-blue-700 dark:bg-blue-800 text-white p-8 md:p-12 flex flex-col md:flex-row justify-between items-center gap-8">
			<!-- Left Side: Image, Name, Title -->
			<div class="flex items-center gap-6 text-center md:text-left" data-aos="fade-right" data-aos-delay="200">
				{#if personalInfo.avatar}
					<img src={personalInfo.avatar} alt={personalInfo.name} class="w-24 h-24 md:w-32 md:h-32 rounded-full border-4 border-white dark:border-gray-700 shadow-lg object-cover transition-transform hover:scale-105 duration-300" />
				{/if}
				<div>
					<h1 class="text-4xl md:text-5xl font-extrabold mb-2">{personalInfo.name}</h1>
					<p class="text-xl md:text-2xl text-blue-100 dark:text-blue-200 font-medium">{personalInfo.title}</p>
				</div>
			</div>
			
			<!-- Right Side: Contact Info -->
			<div class="flex flex-col gap-3 text-sm md:text-base" data-aos="fade-left" data-aos-delay="400">
				<div class="flex items-center justify-center md:justify-start gap-3 group">
					<svg class="w-5 h-5 flex-shrink-0 transition-colors group-hover:text-blue-300" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path></svg>
					<span>{personalInfo.address}</span>
				</div>
				<div class="flex items-center justify-center md:justify-start gap-3 group">
					<svg class="w-5 h-5 flex-shrink-0 transition-colors group-hover:text-blue-300" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path></svg>
					<span>{personalInfo.phone}</span>
				</div>
				<div class="flex items-center justify-center md:justify-start gap-3 group">
					<svg class="w-5 h-5 flex-shrink-0 transition-colors group-hover:text-blue-300" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"></path></svg>
					<a href="mailto:{personalInfo.email}" class="hover:underline hover:text-blue-200 transition-colors">{personalInfo.email}</a>
				</div>
				<div class="flex items-center justify-center md:justify-start gap-3 group">
					<svg class="w-5 h-5 flex-shrink-0 transition-colors group-hover:text-blue-300" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.828 10.172a4 4 0 00-5.656 0l-4 4a4 4 0 105.656 5.656l1.102-1.101m-.758-4.899a4 4 0 005.656 0l4-4a4 4 0 00-5.656-5.656l-1.1 1.1"></path></svg>
					<a href={personalInfo.github} target="_blank" rel="noopener noreferrer" class="hover:underline hover:text-blue-200 transition-colors">GitHub</a>
				</div>
			</div>
		</header>

		<!-- Content -->
		<div class="p-8 md:p-12">
			<div class="grid grid-cols-1 lg:grid-cols-5 gap-12">
				<!-- Left Column (Weight 3) -->
				<div class="lg:col-span-3 space-y-12">
					<!-- Education -->
					<div data-aos="fade-up" data-aos-delay="100">
						<Section title="Học vấn">
							<div class="space-y-10">
								{#each education as edu (edu.major)}
									<TimelineItem
										time={edu.time}
										title={edu.major}
										subtitle={edu.school}
										tasks={edu.achievements}
									/>
								{/each}
							</div>
						</Section>
					</div>

					<!-- Experience -->
					<div data-aos="fade-up" data-aos-delay="200">
						<Section title="Kinh nghiệm làm việc">
							<div class="space-y-10">
								{#each experience as exp (exp.time)}
									<TimelineItem
										time={exp.time}
										title={exp.position}
										subtitle={exp.company}
										tasks={exp.tasks}
									/>
								{/each}
							</div>
						</Section>
					</div>

					<!-- Activities -->
					<div data-aos="fade-up" data-aos-delay="300">
						<Section title="Hoạt động">
							<div class="space-y-8">
								{#each activities as act (act.role)}
									<div class="bg-gray-50 dark:bg-gray-800/50 p-6 rounded-lg border border-gray-100 dark:border-gray-700 hover:shadow-md transition-all">
										<h3 class="text-xl font-bold text-gray-900 dark:text-gray-100">{act.role}</h3>
										<p class="text-blue-600 dark:text-blue-400 font-medium mb-3">{act.organization} | {act.time}</p>
										<ul class="list-disc list-inside text-gray-600 dark:text-gray-400 space-y-1">
											{#each act.tasks as task (task)}
												<li>{task}</li>
											{/each}
										</ul>
									</div>
								{/each}
							</div>
						</Section>
					</div>
				</div>

				<!-- Right Column (Weight 2) -->
				<div class="lg:col-span-2 space-y-12">
					<!-- Objective -->
					<div data-aos="fade-left" data-aos-delay="100">
						<Section title="Mục tiêu nghề nghiệp">
							<p class="italic text-gray-700 dark:text-gray-300 border-l-4 border-blue-600 pl-4 py-2 bg-blue-50 dark:bg-blue-900/20 rounded-r-lg shadow-sm">
								{objective}
							</p>
						</Section>
					</div>

					<!-- Skills -->
					<div data-aos="fade-left" data-aos-delay="200">
						<Section title="Kỹ năng">
							<div class="space-y-4">
								{#each skills as skill (skill.name)}
									<SkillBar name={skill.name} score={skill.score} />
								{/each}
							</div>
						</Section>
					</div>

					<!-- Certificates -->
					<div data-aos="fade-left" data-aos-delay="300">
						<Section title="Chứng chỉ">
							<ul class="list-disc list-inside space-y-3">
								{#each certificates as cert (cert)}
									<li class="text-gray-700 dark:text-gray-400 hover:text-blue-600 dark:hover:text-blue-400 transition-colors cursor-default">{cert}</li>
								{/each}
							</ul>
						</Section>
					</div>

					<!-- Projects -->
					<div data-aos="fade-left" data-aos-delay="400">
						<Section title="Dự án cá nhân">
							<div class="space-y-6">
								{#each projects as proj (proj.name)}
									<ProjectCard
										name={proj.name}
										downloads={proj.downloads}
										tech={proj.tech}
										link={proj.link}
									/>
								{/each}
							</div>
						</Section>
					</div>

					<!-- Hobbies -->
					<div data-aos="fade-left" data-aos-delay="500">
						<Section title="Sở thích">
							<div class="flex flex-wrap gap-2">
								{#each hobbies as hobby (hobby)}
									<span class="bg-gray-100 dark:bg-gray-800 text-gray-800 dark:text-gray-200 px-4 py-2 rounded-lg font-medium hover:bg-blue-100 dark:hover:bg-blue-900/50 hover:text-blue-700 dark:hover:text-blue-300 transition-colors cursor-default">
										{hobby}
									</span>
								{/each}
							</div>
						</Section>
					</div>

					<!-- Additional Info -->
					<div data-aos="fade-left" data-aos-delay="600">
						<Section title="Thông tin thêm">
							<ul class="list-none space-y-4">
								{#each additionalInfo as info (info)}
									<li class="flex items-start gap-3 text-gray-700 dark:text-gray-300 bg-gray-50 dark:bg-gray-800/50 p-4 rounded-lg border border-transparent hover:border-blue-200 dark:hover:border-blue-800 transition-all shadow-sm">
										<svg class="w-6 h-6 text-green-500 flex-shrink-0 mt-0.5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>
										<span>{info}</span>
									</li>
								{/each}
							</ul>
						</Section>
					</div>
				</div>
			</div>
		</div>
	</div>
</main>

<style>
	:global(html.dark) {
		color-scheme: dark;
	}
</style>
