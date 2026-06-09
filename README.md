<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EduControl Pro | Dashboard de Asistencia</title>
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11"></script>
    <script src="https://unpkg.com/html5-qrcode" type="text/javascript"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        body { font-family: 'Inter', sans-serif; transition: background-color 0.3s, color 0.3s; }
        /* Corrección estética para el contenedor del lector QR */
        #reader video { object-fit: cover !important; border-radius: 0.75rem; }
    </style>
</head>
<body class="bg-slate-50 text-slate-900 dark:bg-slate-950 dark:text-slate-50 min-h-screen flex flex-col md:flex-row">

    <aside class="w-full md:w-68 bg-white dark:bg-slate-900 border-b md:border-b-0 md:border-r border-slate-200 dark:border-slate-800 p-6 flex flex-col justify-between shrink-0">
        <div>
            <div class="flex items-center gap-3 mb-8">
                <div class="p-2.5 bg-indigo-600 rounded-xl text-white shadow-md shadow-indigo-500/20">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2m-3 7h3m-3 4h3m-6-4h.01M9 16h.01"/></svg>
                </div>
                <div>
                    <h1 class="text-base font-bold tracking-tight">EduControl v2</h1>
                    <p class="text-xs text-slate-400 dark:text-slate-500">Gestión de Asistencia</p>
                </div>
            </div>

            <button onclick="toggleDarkMode()" class="w-full flex items-center justify-center gap-2 mb-8 py-2.5 px-4 rounded-xl border border-slate-200 dark:border-slate-800 bg-slate-50 dark:bg-slate-800/50 hover:bg-slate-100 dark:hover:bg-slate-800 text-sm font-medium transition cursor-pointer">
                <span class="dark:hidden flex items-center gap-2">🌙 Cambiar a Modo Oscuro</span>
                <span class="hidden dark:flex items-center gap-2">☀️ Cambiar a Modo Claro</span>
            </button>

            <div class="space-y-2">
                <p class="text-[11px] font-bold uppercase tracking-wider text-slate-400 dark:text-slate-500 px-1 mb-2">Respaldo Seguro</p>
                <button onclick="exportarBackup()" class="w-full flex items-center justify-center gap-2 px-4 py-3 rounded-xl bg-emerald-600 hover:bg-emerald-700 text-white text-sm font-semibold transition shadow-sm cursor-pointer">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"/></svg>
                    Exportar Backup (.js)
                </button>
            </div>
        </div>

        <div class="text-[11px] text-slate-400 dark:text-slate-500 pt-4 border-t border-slate-100 dark:border-slate-800 mt-8 md:mt-0">
            Diseño Premium Dashboard &bull; 2026
        </div>
    </aside>

    <main class="flex-1 p-4 md:p-8 space-y-6 max-w-7xl mx-auto w-full overflow-hidden">
        
        <section class="grid grid-cols-1 lg:grid-cols-3 gap-6">
            
            <div class="bg-white dark:bg-slate-900 rounded-2xl border border-slate-200 dark:border-slate-800 p-5 shadow-sm flex flex-col justify-between">
                <div>
                    <div class="flex items-center justify-between mb-3">
                        <h2 class="text-xs font-bold uppercase tracking-wider text-slate-400 dark:text-slate-500 flex items-center gap-2">
                            <span class="w-2 h-2 rounded-full bg-indigo-600 animate-pulse"></span> Terminal QR Nativo
                        </h2>
                        <button onclick="alternarCamara()" id="btn-toggle-cam" class="text-xs text-indigo-600 dark:text-indigo-400 font-semibold hover:underline cursor-pointer">Encender Cámara</button>
                    </div>
                    <div class="relative bg-slate-950 rounded-xl overflow-hidden aspect-video flex items-center justify-center">
                        <div id="reader" class="w-full h-full"></div>
                        <div id="scanner-placeholder" class="absolute inset-0 bg-slate-900 flex flex-col items-center justify-center p-4 text-center z-10">
                            <svg class="w-8 h-8 text-slate-600 mb-2" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M12 4v1m6 11h2m-6 0h-2v4m0-11v3m0 0h.01M12 12h4.01M16 20h4M4 12h4m12 0h.01M5 8h2a1 1 0 001-1V5a1 1 0 00-1-1H5a1 1 0 00-1 1v2a1 1 0 001 1zm12 0h2a1 1 0 001-1V5a1 1 0 00-1-1h-2a1 1 0 00-1 1v2a1 1 0 001 1zM5 20h2a1 1 0 001-1v-2a1 1 0 00-1-1H5a1 1 0 00-1 1v2a1 1 0 001 1z"/></svg>
                            <p class="text-xs text-slate-400">El escáner está apagado</p>
                        </div>
                    </div>
                </div>
                <p class="text-[11px] text-slate-400 dark:text-slate-500 mt-3">Usa códigos QR con el ID del estudiante para el registro express.</p>
            </div>

            <div class="lg:col-span-2 bg-white dark:bg-slate-900 rounded-2xl border border-slate-200 dark:border-slate-800 p-5 shadow-sm flex flex-col justify-between">
                <div>
                    <h2 class="text-xs font-bold uppercase tracking-wider text-slate-400 dark:text-slate-500 mb-4">🔍 Motores de Búsqueda y Criterios</h2>
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                        <div class="sm:col-span-3">
                            <label class="block text-xs font-medium text-slate-400 mb-1">Buscar por descripción (Nombre de Alumno o Tipo de asistencia)</label>
                            <input type="text" id="filtro-buscar" oninput="renderizarAsistencias()" placeholder="Ej. Juan Pérez, Presente, Tarde..." class="w-full p-2.5 bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl text-sm focus:outline-none focus:border-indigo-500 dark:focus:border-indigo-400 transition">
                        </div>
                        <div>
                            <label class="block text-xs font-medium text-slate-400 mb-1">Fecha Específica</label>
                            <input type="date" id="filtro-fecha" onchange="renderizarAsistencias()" class="w-full p-2.5 bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl text-sm focus:outline-none focus:border-indigo-500 transition">
                        </div>
                        <div>
                            <label class="block text-xs font-medium text-slate-400 mb-1">Categoría / Especialidad</label>
                            <select id="filtro-categoria" onchange="renderizarAsistencias()" class="w-full p-2.5 bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 rounded-xl text-sm focus:outline-none focus:border-indigo-500 transition">
                                <option value="Todos">Todas las Especialidades</option>
                                <option value="Contabilidad">Contabilidad</option>
                                <option value="Administración">Administración</option>
                            </select>
                        </div>
                        <div class="flex items-end">
                            <button onclick="limpiarFiltros()" class="w-full py-2.5 px-4 bg-slate-100 hover:bg-slate-200 dark:bg-slate-800 dark:hover:bg-slate-700 text-slate-700 dark:text-slate-300 rounded-xl text-sm font-semibold transition cursor-pointer">
                                Reestablecer Filtros
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section class="bg-white dark:bg-slate-900 rounded-2xl border border-slate-200 dark:border-slate-800 shadow-sm overflow-hidden">
            <div class="p-5 border-b border-slate-100 dark:border-slate-800 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-3">
                <div>
                    <h2 class="text-base font-bold">Listado Operativo de Alumnos</h2>
                    <p class="text-xs text-slate-400">Modifica, añade o elimina alumnos del registro escolar.</p>
                </div>
                <button onclick="agregarEstudianteForm()" class="px-4 py-2 bg-indigo-600 hover:bg-indigo-700 text-white rounded-xl text-xs font-semibold transition shadow-sm cursor-pointer">
                    + Registrar Nuevo Alumno
                </button>
            </div>
            <div class="overflow-x-auto max-h-72">
                <table class="w-full text-left border-collapse text-sm">
                    <thead class="bg-slate-50/70 dark:bg-slate-800/40 text-slate-400 text-xs font-semibold uppercase tracking-wider sticky top-0 backdrop-blur-md z-20">
                        <tr>
                            <th class="p-4">ID</th>
                            <th class="p-4">Estudiante</th>
                            <th class="p-4">Categoría</th>
                            <th class="p-4 text-right">Acciones de Gestión</th>
                        </tr>
                    </thead>
                    <tbody id="tabla-estudiantes" class="divide-y divide-slate-100 dark:divide-slate-800">
                        </tbody>
                </table>
            </div>
        </section>

        <section class="bg-white dark:bg-slate-900 rounded-2xl border border-slate-200 dark:border-slate-800 shadow-sm overflow-hidden">
            <div class="p-5 border-b border-slate-100 dark:border-slate-800 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-3">
                <div>
                    <h2 class="text-base font-bold">Control y Seguimiento de Asistencias</h2>
                    <p class="text-xs text-slate-400">Historial activo indexado (30 registros históricos iniciales de control).</p>
                </div>
                <button onclick="crearAsistenciaManualForm()" class="px-4 py-2 bg-amber-600 hover:bg-amber-700 text-white rounded-xl text-xs font-semibold transition shadow-sm cursor-pointer">
                    + Insertar Registro Manual
                </button>
            </div>
            <div class="overflow-x-auto max-h-96">
                <table class="w-full text-left border-collapse text-sm">
                    <thead class="bg-slate-50/70 dark:bg-slate-800/40 text-slate-400 text-xs font-semibold uppercase tracking-wider sticky top-0 backdrop-blur-md z-20">
                        <tr>
                            <th class="p-4">Fecha y Hora</th>
                            <th class="p-4">Estudiante</th>
                            <th class="p-4">Categoría</th>
                            <th class="p-4">Tipo / Estado</th>
                            <th class="p-4 text-right">Acciones</th>
                        </tr>
                    </thead>
                    <tbody id="tabla-asistencias" class="divide-y divide-slate-100 dark:divide-slate-800">
                        </tbody>
                </table>
            </div>
        </section>

    </main>

    <script>
        // --- BASE DE DATOS LOCAL PRECARGADA CON LOS 20 ESTUDIANTES ---
        const estudiantesBase = [
            { id: 101, nombre: "Juan Pérez Ramos", categoria: "Contabilidad" },
            { id: 102, nombre: "María Gomez Soler", categoria: "Contabilidad" },
            { id: 103, nombre: "Carlos Flores Mendoza", categoria: "Administración" },
            { id: 104, nombre: "Ana Torres Castro", categoria: "Contabilidad" },
            { id: 105, nombre: "Luis Castillo Vega", categoria: "Administración" },
            { id: 106, nombre: "Sofía Medina Ortiz", categoria: "Contabilidad" },
            { id: 107, nombre: "Diego Peralta Rojas", categoria: "Contabilidad" },
            { id: 108, nombre: "Laura Vega Benítez", categoria: "Administración" },
            { id: 109, nombre: "Pedro Campos Arce", categoria: "Contabilidad" },
            { id: 110, nombre: "Elena Diaz Pardo", categoria: "Administración" },
            { id: 111, nombre: "Miguel Rivas Peña", categoria: "Contabilidad" },
            { id: 112, nombre: "Clara Mendoza Luna", categoria: "Contabilidad" },
            { id: 113, nombre: "Jorge Soto Villarreal", categoria: "Administración" },
            { id: 114, nombre: "Patricia Lara Quiroz", categoria: "Contabilidad" },
            { id: 115, nombre: "Roberto Luna Fuentes", categoria: "Administración" },
            { id: 116, nombre: "Natalia Cruz Saldaña", categoria: "Contabilidad" },
            { id: 117, nombre: "Gabriel Rios Tello", categoria: "Contabilidad" },
            { id: 118, nombre: "Lucia Solis Miranda", categoria: "Administración" },
            { id: 119, nombre: "Andrés Silva Duarte", categoria: "Contabilidad" },
            { id: 120, nombre: "Sonia Peña Palacios", categoria: "Administración" }
        ];

        // Construcción interactiva automatizada de exactamente 30 registros distribuidos
        let asistenciasBase = [];
        let controlFecha = new Date();
        for (let i = 1; i <= 30; i++) {
            let alumno = estudiantesBase[i % 20];
            let f = new Date(controlFecha);
            f.setDate(f.getDate() - Math.floor(i / 3)); 
            asistenciasBase.push({
                id: 5000 + i,
                idEstudiante: alumno.id,
                fecha: f.toISOString().split('T')[0] + " " + f.toTimeString().split(' ')[0].substring(0,5),
                estado: i % 6 === 0 ? "Tarde" : "Presente"
            });
        }

        // Persistencia y estados dinámicos mediante LocalStorage
        let estudiantes = JSON.parse(localStorage.getItem('edu_estudiantes')) || estudiantesBase;
        let asistencias = JSON.parse(localStorage.getItem('edu_asistencias')) || asistenciasBase;
        let html5QrcodeScanner = null;

        function sincronizarLocalStorage() {
            localStorage.setItem('edu_estudiantes', JSON.stringify(estudiantes));
            localStorage.setItem('edu_asistencias', JSON.stringify(asistencias));
        }

        // --- MANEJO DEL CONTROLLER TEMA OSCURO NATIVO ---
        if (localStorage.getItem('theme') === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
            document.documentElement.classList.add('dark');
        } else {
            document.documentElement.classList.remove('dark');
        }

        function toggleDarkMode() {
            if (document.documentElement.classList.contains('dark')) {
                document.documentElement.classList.remove('dark');
                localStorage.setItem('theme', 'light');
            } else {
                document.documentElement.classList.add('dark');
                localStorage.setItem('theme', 'dark');
            }
        }

        // --- RENDERIZADORES DE INTERFAZ ---
        function renderizarEstudiantes() {
            const container = document.getElementById('tabla-estudiantes');
            container.innerHTML = '';
            estudiantes.forEach(est => {
                container.innerHTML += `
                    <tr class="hover:bg-slate-50/60 dark:hover:bg-slate-800/40 transition">
                        <td class="p-4 font-mono font-bold text-xs text-indigo-600 dark:text-indigo-400">#${est.id}</td>
                        <td class="p-4 font-medium text-slate-800 dark:text-slate-200">${est.nombre}</td>
                        <td class="p-4">
                            <span class="px-2.5 py-1 rounded-lg text-xs font-semibold ${est.categoria === 'Contabilidad' ? 'bg-blue-50 text-blue-700 dark:bg-blue-900/30 dark:text-blue-300' : 'bg-purple-50 text-purple-700 dark:bg-purple-900/30 dark:text-purple-300'}">
                                ${est.categoria}
                            </span>
                        </td>
                        <td class="p-4 text-right space-x-3">
                            <button onclick="editarEstudianteForm(${est.id})" class="text-indigo-600 dark:text-indigo-400 hover:underline font-medium text-xs cursor-pointer">Editar</button>
                            <button onclick="eliminarEstudiante(${est.id})" class="text-rose-500 hover:underline font-medium text-xs cursor-pointer">Eliminar</button>
                        </td>
                    </tr>
                `;
            });
        }

        function renderizarAsistencias() {
            const container = document.getElementById('tabla-asistencias');
            const term = document.getElementById('filtro-buscar').value.toLowerCase();
            const fFecha = document.getElementById('filtro-fecha').value;
            const fCat = document.getElementById('filtro-categoria').value;

            container.innerHTML = '';

            let filtrados = asistencias.filter(asist => {
                let est = estudiantes.find(e => e.id == asist.idEstudiante);
                let nombre = est ? est.nombre.toLowerCase() : 'retirado';
                let estd = asist.estado.toLowerCase();

                let matchTerm = nombre.includes(term) || estd.includes(term);
                let matchFecha = fFecha ? asist.fecha.startsWith(fFecha) : true;
                let matchCat = fCat !== "Todos" ? (est && est.categoria === fCat) : true;

                return matchTerm && matchFecha && matchCat;
            });

            filtrados.sort((a,b) => b.fecha.localeCompare(a.fecha));

            if(filtrados.length === 0) {
                container.innerHTML = `<tr><td colspan="5" class="p-8 text-center text-slate-400 text-xs">No se encontraron registros de asistencias con los filtros aplicados.</td></tr>`;
                return;
            }

            filtrados.forEach(asist => {
                let est = estudiantes.find(e => e.id == asist.idEstudiante);
                container.innerHTML += `
                    <tr class="hover:bg-slate-50/60 dark:hover:bg-slate-800/40 transition">
                        <td class="p-4 text-xs font-mono text-slate-500">${asist.fecha}</td>
                        <td class="p-4 font-medium">${est ? est.nombre : '<em class="text-slate-400">Alumno Retirado</em>'}</td>
                        <td class="p-4 text-xs text-slate-500">${est ? est.categoria : '-'}</td>
                        <td class="p-4">
                            <span class="px-2.5 py-0.5 rounded-full text-xs font-semibold ${asist.estado === 'Presente' ? 'bg-emerald-50 text-emerald-700 dark:bg-emerald-950 dark:text-emerald-400' : 'bg-amber-50 text-amber-700 dark:bg-amber-950 dark:text-amber-400'}">
                                ${asist.estado}
                            </span>
                        </td>
                        <td class="p-4 text-right space-x-2">
                            <button onclick="editarAsistenciaForm(${asist.id})" class="text-slate-400 hover:text-slate-700 dark:hover:text-slate-200 text-xs cursor-pointer">Editar</button>
                            <button onclick="eliminarAsistencia(${asist.id})" class="text-rose-400 hover:text-rose-600 text-xs cursor-pointer">❌</button>
                        </td>
                    </tr>
                `;
            });
        }

        function limpiarFiltros() {
            document.getElementById('filtro-buscar').value = '';
            document.getElementById('filtro-fecha').value = '';
            document.getElementById('filtro-categoria').value = 'Todos';
            renderizarAsistencias();
        }

        // --- ACCIONES FORMULARIOS INTERACTIVOS (CRUD ALUMNOS) ---
        async function agregarEstudianteForm() {
            const { value: formValues } = await Swal.fire({
                title: 'Matricula de Estudiante',
                html: `
                    <input id="sw-id" type="number" placeholder="Código ID Único (Ej: 121)" class="swal2-input">
                    <input id="sw-nombre" type="text" placeholder="Apellidos y Nombres Completos" class="swal2-input">
                    <select id="sw-cat" class="swal2-input"><option value="Contabilidad">Contabilidad</option><option value="Administración">Administración</option></select>
                `,
                confirmButtonText: 'Registrar',
                showCancelButton: true,
                focusConfirm: false,
                preConfirm: () => ({
                    id: parseInt(document.getElementById('sw-id').value),
                    nombre: document.getElementById('sw-nombre').value,
                    categoria: document.getElementById('sw-cat').value
                })
            });

            if (formValues) {
                if(!formValues.id || !formValues.nombre) return Swal.fire('Error', 'Todos los campos son obligatorios', 'warning');
                if(estudiantes.some(e => e.id === formValues.id)) return Swal.fire('Error Duplicado', 'Esta ID ya se encuentra asignada', 'error');

                estudiantes.push(formValues);
                sincronizarLocalStorage(); renderizarEstudiantes();
                Swal.fire('Registrado', 'Estudiante añadido exitosamente.', 'success');
            }
        }

        async function editarEstudianteForm(id) {
            let est = estudiantes.find(e => e.id === id);
            const { value: formValues } = await Swal.fire({
                title: 'Actualizar Datos Alumno',
                html: `
                    <input id="sw-edit-nombre" type="text" value="${est.nombre}" class="swal2-input">
                    <select id="sw-edit-cat" class="swal2-input">
                        <option value="Contabilidad" ${est.categoria === 'Contabilidad' ? 'selected' : ''}>Contabilidad</option>
                        <option value="Administración" ${est.categoria === 'Administración' ? 'selected' : ''}>Administración</option>
                    </select>
                `,
                confirmButtonText: 'Guardar Cambios',
                showCancelButton: true,
                preConfirm: () => ({
                    nombre: document.getElementById('sw-edit-nombre').value,
                    categoria: document.getElementById('sw-edit-cat').value
                })
            });

            if(formValues) {
                est.nombre = formValues.nombre;
                est.categoria = formValues.categoria;
                sincronizarLocalStorage(); renderizarEstudiantes(); renderizarAsistencias();
                Swal.fire('Actualizado', 'Datos actualizados en el sistema', 'success');
            }
        }

        function eliminarEstudiante(id) {
            Swal.fire({
                title: '¿Dar de baja al Alumno?',
                text: "Se eliminará del listado pero su histórico de asistencias permanecerá.",
                icon: 'warning',
                showCancelButton: true,
                confirmButtonColor: '#f43f5e',
                confirmButtonText: 'Sí, remover'
            }).then(result => {
                if(result.isConfirmed) {
                    estudiantes = estudiantes.filter(e => e.id !== id);
                    sincronizarLocalStorage(); renderizarEstudiantes(); renderizarAsistencias();
                    Swal.fire('Eliminado', 'Registro purgado', 'success');
                }
            });
        }

        // --- LOGICA DE CONTROL DE ASISTENCIAS ---
        function ejecutarRegistroExpressQR(idLeido) {
            let alumno = estudiantes.find(e => e.id == idLeido);
            if(!alumno) {
                Swal.fire('QR Desconocido', `El código ID #${idLeido} no está matriculado.`, 'error');
                return;
            }

            let ahora = new Date();
            asistencias.push({
                id: Date.now(),
                idEstudiante: alumno.id,
                fecha: ahora.toISOString().split('T')[0] + " " + ahora.toTimeString().split(' ')[0].substring(0,5),
                estado: "Presente"
            });

            sincronizarLocalStorage(); renderizarAsistencias();
            Swal.fire({
                title: '¡Asistencia QR Registrada!',
                text: alumno.nombre,
                icon: 'success',
                timer: 1500,
                showConfirmButton: false
            });
        }

        async function crearAsistenciaManualForm() {
            let options = estudiantes.map(e => `<option value="${e.id}">${e.nombre}</option>`).join('');
            let hoy = new Date().toISOString().split('T')[0];

            const { value: formValues } = await Swal.fire({
                title: 'Nueva Ficha de Asistencia',
                html: `
                    <select id="man-est" class="swal2-input">${options}</select>
                    <input id="man-fecha" type="datetime-local" class="swal2-input" value="${hoy}T08:00">
                    <select id="man-estado" class="swal2-input"><option value="Presente">Presente</option><option value="Tarde">Tarde</option></select>
                `,
                preConfirm: () => ({
                    idEstudiante: parseInt(document.getElementById('man-est').value),
                    fecha: document.getElementById('man-fecha').value.replace('T', ' '),
                    estado: document.getElementById('man-estado').value
                })
            });

            if(formValues) {
                formValues.id = Date.now();
                asistencias.push(formValues);
                sincronizarLocalStorage(); renderizarAsistencias();
                Swal.fire('Éxito', 'Registro insertado en la bitácora', 'success');
            }
        }

        async function editarAsistenciaForm(id) {
            let asist = asistencias.find(a => a.id === id);
            let rawFecha = asist.fecha.replace(' ', 'T');

            const { value: formValues } = await Swal.fire({
                title: 'Modificar Bitácora de Asistencia',
                html: `
                    <input id="ed-as-fecha" type="datetime-local" value="${rawFecha}" class="swal2-input">
                    <select id="ed-as-estado" class="swal2-input">
                        <option value="Presente" ${asist.estado === 'Presente' ? 'selected' : ''}>Presente</option>
                        <option value="Tarde" ${asist.estado === 'Tarde' ? 'selected' : ''}>Tarde</option>
                    </select>
                `,
                preConfirm: () => ({
                    fecha: document.getElementById('ed-as-fecha').value.replace('T', ' '),
                    estado: document.getElementById('ed-as-estado').value
                })
            });

            if(formValues) {
                asist.fecha = formValues.fecha;
                asist.estado = formValues.estado;
                sincronizarLocalStorage(); renderizarAsistencias();
                Swal.fire('Guardado', 'Cambios guardados', 'success');
            }
        }

        function eliminarAsistencia(id) {
            asistencias = asistencias.filter(a => a.id !== id);
            sincronizarLocalStorage(); renderizarAsistencias();
        }

        // --- SISTEMA DE CAMARA NATIVA (HTML5-QRCODE) ---
        function alternarCamara() {
            const btn = document.getElementById('btn-toggle-cam');
            const placeholder = document.getElementById('scanner-placeholder');

            if (!html5QrcodeScanner) {
                html5QrcodeScanner = new Html5Qrcode("reader");
                
                // Configuración ideal para apertura fluida en dispositivos móviles modernos
                html5QrcodeScanner.start(
                    { facingMode: "environment" }, // Abre la cámara trasera por defecto
                    { fps: 15, qrbox: { width: 250, height: 250 } },
                    (qrCodeMessage) => {
                        ejecutarRegistroExpressQR(qrCodeMessage.trim());
                    },
                    (errorMessage) => { /* Silenciar logs recurrentes de búsqueda en tiempo real */ }
                ).then(() => {
                    placeholder.style.display = 'none';
                    btn.innerText = "Apagar Cámara";
                    btn.classList.replace('text-indigo-600', 'text-rose-500');
                }).catch(err => {
                    console.error(err);
                    Swal.fire('Permisos Denegados', 'No se pudo acceder a la cámara trasera del dispositivo móvil.', 'error');
                    html5QrcodeScanner = null;
                });
            } else {
                html5QrcodeScanner.stop().then(() => {
                    html5QrcodeScanner = null;
                    placeholder.style.display = 'flex';
                    btn.innerText = "Encender Cámara";
                    btn.classList.replace('text-rose-500', 'text-indigo-600');
                });
            }
        }

        // --- RESPALDO EXPORTABLE (.JS) ---
        function exportarBackup() {
            let jsDoc = `/** ARCHIVO DE RESPALDO DE SEGURIDAD - EDUCONTROL **/\n`;
            jsDoc += `// Fecha de creación: ${new Date().toLocaleString()}\n\n`;
            jsDoc += `const BACKUP_ESTUDIANTES = ${JSON.stringify(estudiantes, null, 4)};\n\n`;
            jsDoc += `const BACKUP_ASISTENCIAS = ${JSON.stringify(asistencias, null, 4)};\n`;

            const blob = new Blob([jsDoc], { type: 'text/javascript' });
            const link = document.createElement('a');
            link.href = URL.createObjectURL(blob);
            link.download = `backup_asistencia_${new Date().toISOString().split('T')[0]}.js`;
            link.click();
            URL.revokeObjectURL(link.href);
        }

        // Inicialización General
        window.addEventListener('DOMContentLoaded', () => {
            renderizarEstudiantes();
            renderizarAsistencias();
        });
    </script>
</body>
</html>
