import React, { useState, useEffect } from 'react';
import { initializeApp } from 'firebase/app';
import { getFirestore, collection, doc, onSnapshot, addDoc, setDoc } from 'firebase/firestore';
import { getAuth, signInAnonymously, onAuthStateChanged, signInWithCustomToken } from 'firebase/auth';

// --- Firebase 設定 ---
const firebaseConfig = typeof __firebase_config !== 'undefined' 
    ? JSON.parse(__firebase_config) 
    : {
        apiKey: "YOUR_API_KEY",
        authDomain: "YOUR_AUTH_DOMAIN",
        projectId: "YOUR_PROJECT_ID",
        storageBucket: "YOUR_STORAGE_BUCKET",
        messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
        appId: "YOUR_APP_ID"
    };
    
const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';

// 為了預覽，暫時註解 Firebase 初始化
// const app = initializeApp(firebaseConfig);
// const db = getFirestore(app);
// const auth = getAuth(app);

// --- 模擬資料 ---
const mockRfqData = [
    { id: 'NRFQ202503004', customer: 'Marquee', model: 'ED055TC1', sales: 'Meg Chen', pm: 'Luke Lu', status: 'Approved', applicationDate: '2025-03-12', asp: 1238, cogs: 879, materialsCost: 580, laborCost: 250, overhead: 49 },
    { id: 'NRFQ202508007', customer: 'TPV Electronics', model: 'ED312TT2', sales: 'Lily Lien', pm: 'LK Tseng', status: 'Rejected', applicationDate: '2025-08-26', asp: 299, cogs: 251, materialsCost: 180, laborCost: 50, overhead: 21 },
    { id: 'NRFQ202507010', customer: 'Agile Display', model: 'ED315SP6', sales: 'Lily Lien', pm: 'Luke Lu', status: 'Approved', applicationDate: '2025-07-14', asp: 300, cogs: 251, materialsCost: 185, laborCost: 46, overhead: 20 },
];

const mockProjects = [
    { id: 'proj001', modelName: 'ED055TC1', productId: 'ED843921', status: 'NPDA', rfqId: 'NRFQ202503004', progress: 45, milestones: { start: '2025-09-01', ws: '2025-11-15', es: '2026-02-20', pp: '2026-05-10', mp: '2026-08-01' } },
    { id: 'proj002', modelName: 'ED210TC8', productId: 'ED583291', status: 'NPA Meeting', rfqId: 'NRFQ202502011', progress: 75, milestones: { start: '2025-07-15', ws: '2025-09-25', es: '2025-12-15', pp: '2026-03-20', mp: '2026-06-15' } },
    { id: 'proj003', modelName: 'ES103TC1', productId: 'ES103852', status: 'MP', rfqId: 'NRFQ202411034', progress: 100, milestones: { start: '2025-04-01', ws: '2025-06-10', es: '2025-08-20', pp: '2025-10-30', mp: '2026-01-20' } },
    { id: 'proj004', modelName: 'ED078KC1', productId: 'ED912345', status: 'NPDA', rfqId: 'NRFQ202506005', progress: 20, milestones: { start: '2025-10-01', ws: '2025-12-20', es: '2026-03-15', pp: '2026-06-01', mp: '2026-09-01' } },
];

// --- 表單選項 ---
const formOptions = {
    application: ['eNote', 'eReader', 'Logistics', 'Signage', 'Segmented', 'Retail'],
    npdaType: [
        { value: 'Type A', label: 'Type A- 關鍵元件(TFT, CF, FPL, FL, TP)中一項或多項為新設計，且 TFT 有委外需求' },
        { value: 'Type B', label: 'Type B- 關鍵元件(TFT, CF, FPL, FL, TP)中一項或多項為新設計' },
        { value: 'Type C', label: 'Type C- 使用現有關鍵元件，但有新的結構堆疊' },
        { value: 'Type D', label: 'Type D- 僅開發 TFT' },
        { value: 'Type E', label: 'Type E- 使用現有關鍵元件與既有堆疊結構' },
        { value: 'Type F', label: 'Type F- Segment 相關產品' },
        { value: 'Type G', label: 'Type G- 特定尺寸 FPL 裁切' },
        { value: 'Type H', label: 'Type H- Module 採 Buy and Sell 模式' },
        { value: 'Type I', label: 'Type I- OEM' },
    ],
    tftSubstrate: ['Glass', 'Flex-E', 'S-Flex', 'Prism', 'Others'],
    moduleStructureComponents: ['FPL', 'PS', 'TP', 'FL', 'CL', 'EMR', 'TFT only'],
    specialStructure: ['NA', 'OTFT', 'CFA', 'ACP', 'Kaleido'],
    displayType: ['EPD', 'TFT-LCD', 'OLED'],
    fpl: ['ACeP1', 'ACeP2', 'Spectra 6', 'Carta 1200', 'Other'],
    ps: ['APS195', 'APS200', 'None', 'Other'],
    fl: ['有', '無'],
    cl: ['有', '無', 'NA'],
    tftVendor: ['AUO', 'Innolux', 'BOE', 'CSOT', 'TBD', 'Other'],
    fpc: ['FPC Type 1', 'FPC Type 2', 'N/A'],
    icBonding: ['COG', 'COF', 'N/A'],
    touchSenser: ['Capacitive', 'EMR', 'None', 'Other'],
    reliabilityRequirement: ['Standard', 'Automotive Grade', 'Custom', 'Other'],
    safetyRequirement: ['UL', 'CE', 'None', 'Other'],
    envSubstances: ['EU RoHS', 'EU REACH', 'Sony SS-00259', 'EICC', 'China VoGs'],
    consigned: ['Yes', 'No'],
    customerAttribute: ['Existing', 'New', 'Potential'],
    position: ['Exclusive', 'Dominant', 'Shared', 'Zero'],
    confidenceToEarnBusiness: ['High Confidence', 'Medium Confidence', 'Low Confidence'],
    existingCompetitors: ['Competitor A', 'Competitor B', 'None', 'Other'],
    productSubstitutions: ['Substitution X', 'Substitution Y', 'None', 'Other'],
    yesNo: ['Yes', 'No'],
    materialStandard: ['Standard', 'New', 'NA'],
};

// --- Icon 元件 ---
const Icon = ({ name, className }) => {
    const icons = {
        dashboard: <path strokeLinecap="round" strokeLinejoin="round" d="M3.75 6A2.25 2.25 0 016 3.75h2.25A2.25 2.25 0 0110.5 6v2.25a2.25 2.25 0 01-2.25 2.25H6a2.25 2.25 0 01-2.25-2.25V6zM3.75 15.75A2.25 2.25 0 016 13.5h2.25a2.25 2.25 0 012.25 2.25V18a2.25 2.25 0 01-2.25 2.25H6A2.25 2.25 0 013.75 18v-2.25zM13.5 6a2.25 2.25 0 012.25-2.25H18A2.25 2.25 0 0120.25 6v2.25A2.25 2.25 0 0118 10.5h-2.25a2.25 2.25 0 01-2.25-2.25V6zM13.5 15.75a2.25 2.25 0 012.25-2.25H18a2.25 2.25 0 012.25 2.25V18A2.25 2.25 0 0118 20.25h-2.25A2.25 2.25 0 0113.5 18v-2.25z" />,
        plus: <path strokeLinecap="round" strokeLinejoin="round" d="M12 9v6m3-3H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z" />,
        projects: <path strokeLinecap="round" strokeLinejoin="round" d="M3.75 12h16.5m-16.5 3.75h16.5M3.75 19.5h16.5M5.625 4.5h12.75a1.875 1.875 0 010 3.75H5.625a1.875 1.875 0 010-3.75z" />,
        schedule: <path strokeLinecap="round" strokeLinejoin="round" d="M6.75 3v2.25M17.25 3v2.25M3 18.75V7.5a2.25 2.25 0 012.25-2.25h13.5A2.25 2.25 0 0121 7.5v11.25m-18 0A2.25 2.25 0 005.25 21h13.5A2.25 2.25 0 0021 18.75m-18 0H21" />,
        link: <path strokeLinecap="round" strokeLinejoin="round" d="M13.19 8.688a4.5 4.5 0 011.242 7.244l-4.5 4.5a4.5 4.5 0 01-6.364-6.364l1.757-1.757m13.35-.622l1.757-1.757a4.5 4.5 0 00-6.364-6.364l-4.5 4.5a4.5 4.5 0 001.242 7.244" />,
        chevronDown: <path strokeLinecap="round" strokeLinejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />,
        chevronUp: <path strokeLinecap="round" strokeLinejoin="round" d="M4.5 15.75l7.5-7.5 7.5 7.5" />,
        arrowUp: <path strokeLinecap="round" strokeLinejoin="round" d="M4.5 10.5L12 3m0 0l7.5 7.5M12 3v18" />,
        arrowDown: <path strokeLinecap="round" strokeLinejoin="round" d="M19.5 13.5L12 21m0 0l-7.5-7.5M12 21V3" />
    };
    return ( <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" strokeWidth={1.5} stroke="currentColor" className={className}>{icons[name]}</svg> );
};

// --- 主應用程式元件 ---
export default function App() {
    const [view, setView] = useState('dashboard');
    const [projects, setProjects] = useState([]);
    const [selectedProject, setSelectedProject] = useState(null);
    const [selectedRfq, setSelectedRfq] = useState(null);
    const [user, setUser] = useState(null);
    const [isAuthReady, setIsAuthReady] = useState(false);

    // 模擬 Firebase onSnapshot
    useEffect(() => {
        setProjects(mockProjects);
        setIsAuthReady(true);
    }, []);

    const handleNavigate = (targetView, data = null) => {
        if (targetView === 'npdaForm') {
            if (data?.id) { // Editing existing project
                const fullProjectData = {
                    ...initialFormData,
                    ...data,
                    modelName: data.modelName,
                    rfqId: data.rfqId,
                };
                setSelectedProject(fullProjectData);
                setSelectedRfq(null);
            } else if (data?.rfqId) { // Creating from RFQ
                setSelectedRfq(data.rfqData);
                setSelectedProject(null);
            }
        } else {
            setSelectedProject(data);
            setSelectedRfq(null);
        }
        setView(targetView);
    };

    const handleSaveProject = async (projectData) => {
        alert("專案已儲存 (請查看 console log)");
        console.log("Saved Project Data:", projectData);
        setView('dashboard');
        setSelectedProject(null);
        setSelectedRfq(null);
    };
    
    const renderView = () => {
        if (!isAuthReady) return <div className="flex items-center justify-center h-full"><p>Loading...</p></div>;
        switch (view) {
            case 'rfqSelection': return <RFQSelection onSelectRfq={(rfq) => handleNavigate('npdaForm', { rfqId: rfq.id, rfqData: rfq })} />;
            case 'npdaForm': return <NPDAForm project={selectedProject} rfq={selectedRfq} onSave={handleSaveProject} onCancel={() => handleNavigate('dashboard')} />;
            case 'npaReport': return <NPAReport project={selectedProject} onBack={() => handleNavigate('dashboard')} />;
            case 'scheduleTracking': return <ScheduleTracking projects={projects} />;
            default: return <Dashboard projects={projects} onSelectProject={(p) => handleNavigate('npaReport', p)} onEditProject={(p) => handleNavigate('npdaForm', p)} />;
        }
    };

    return (
        <div className="flex h-screen bg-slate-100 font-sans">
            <Sidebar currentView={view} onNavigate={handleNavigate} />
            <div className="flex-1 flex flex-col overflow-hidden">
                <main className="flex-1 overflow-x-hidden overflow-y-auto p-4 md:p-8">
                    <Header view={view} />
                    <div className="mt-8">{renderView()}</div>
                </main>
            </div>
        </div>
    );
}

// --- 側邊攔元件 ---
const Sidebar = ({ currentView, onNavigate }) => {
    const NavItem = ({ icon, label, viewName, rfq = false }) => {
        const isActive = currentView === viewName || (rfq && ['npdaForm', 'rfqSelection'].includes(currentView));
        return ( <button onClick={() => onNavigate(viewName)} className={`flex items-center w-full px-4 py-3 text-left transition-colors duration-200 rounded-lg ${ isActive ? 'bg-red-50 text-red-700' : 'text-slate-500 hover:bg-slate-200 hover:text-slate-800' }`}><Icon name={icon} className={`h-6 w-6 mr-3 ${isActive ? 'text-red-700' : 'text-slate-400'}`} /> <span className="font-medium">{label}</span></button> );
    };
    const NavLink = ({ icon, label, href }) => ( <a href={href} target="_blank" rel="noopener noreferrer" className="flex items-center w-full px-4 py-3 text-left text-slate-500 hover:bg-slate-200 hover:text-slate-800 transition-colors duration-200 rounded-lg"><Icon name={icon} className="h-6 w-6 mr-3 text-slate-400" /> <span className="font-medium">{label}</span></a> );
    const MenuHeader = ({ label }) => <h3 className="px-4 pt-6 pb-2 text-xs font-semibold text-slate-400 uppercase tracking-wider">{label}</h3>;

    return (
        <aside className="w-64 bg-white border-r border-slate-200 p-4 flex flex-col">
            <div className="text-xl font-bold text-red-700 mb-6 px-2">E Ink PM Platform</div>
            <nav className="flex flex-col space-y-1">
                <MenuHeader label="Overview" />
                <NavItem icon="dashboard" label="Dashboard" viewName="dashboard" />
                
                <MenuHeader label="Project Center" />
                <NavItem icon="plus" label="NPDA Application" viewName="rfqSelection" rfq={true}/>
                <NavItem icon="projects" label="My Projects" viewName="dashboard" />
                <NavItem icon="schedule" label="Schedule Tracking" viewName="scheduleTracking" />
                
                <MenuHeader label="Quick Links" />
                <NavLink icon="link" label="RFQ 2.0" href="https://eih1fr01.eih.eink.com/webappsite/WebForm/Framework/default.aspx?PageUrl=../Engineering/NRFQMain.aspx&LeftBarStatus=Hidden" />
                <NavLink icon="link" label="NPA Model List" href="http://eih1eim02.eih.eink.com/EIM/#/NPAModel" />
                <NavLink icon="link" label="Standard Model List" href="http://eih1scm02dev/PNM/#/ModelInfo" />
                <NavLink icon="link" label="Legacy NPDA" href="https://eih1fr01.eih.eink.com/webappsite/WebForm/Engineering/NPDAMain.aspx" />
                <NavLink icon="link" label="Yield Platform" href="http://myscm.eih.eink.com/Starfish/#/YieldPlatform" />
            </nav>
        </aside>
    );
};

// --- 頁首元件 ---
const Header = ({ view }) => {
    const titles = {
        dashboard: { title: "Dashboard", subtitle: "管理和追蹤所有進行中的專案"},
        rfqSelection: { title: "建立新專案", subtitle: "選擇一個 RFQ 以開始新的 NPDA 專案"},
        npdaForm: { title: "新產品開發申請 (NPDA)", subtitle: "完成並提交新產品的申請"},
        npaReport: { title: "NPA 報告", subtitle: "預覽並準備用於新產品評估會議的報告"},
        scheduleTracking: { title: "時程追蹤", subtitle: "可視化所有活動專案的開發時程"}
    };
    const { title, subtitle } = titles[view] || { title: "PM Platform", subtitle: "新產品開發管理中心" };
    return ( <div className="px-4 sm:px-6 lg:px-8"><h1 className="text-3xl font-bold text-slate-900">{title}</h1><p className="mt-1 text-lg text-slate-500">{subtitle}</p></div> );
};

// --- UI 基礎元件 ---
const Card = ({ children, className = '' }) => ( <div className={`bg-white border border-slate-200/80 rounded-xl shadow-md ${className}`}>{children}</div> );

// --- RFQ 選擇元件 ---
const RFQSelection = ({ onSelectRfq }) => {
    const [expandedRfq, setExpandedRfq] = useState(null);
    const toggleExpand = (rfqId) => setExpandedRfq(expandedRfq === rfqId ? null : rfqId);
    const CostRow = ({ label, value }) => ( <div className="flex justify-between py-1 border-b border-slate-200"><span className="text-slate-500">{label}:</span><span className="font-medium text-slate-700">${value}</span></div> );

    return (
        <div className="px-4 sm:px-6 lg:px-8">
            <Card>
                <div className="overflow-x-auto">
                    <table className="min-w-full divide-y divide-slate-200">
                        <thead className="bg-slate-50"><tr><th scope="col" className="w-12 px-6 py-3"></th><th scope="col" className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">RFQ No.</th><th scope="col" className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Customer</th><th scope="col" className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Model</th><th scope="col" className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">PM</th><th scope="col" className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Status</th><th scope="col" className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Application Date</th><th scope="col" className="relative px-6 py-3"><span className="sr-only">Create NPDA</span></th></tr></thead>
                        <tbody className="bg-white divide-y divide-slate-200">
                            {mockRfqData.map(rfq => (
                                <React.Fragment key={rfq.id}>
                                    <tr className="hover:bg-slate-50 transition-colors">
                                        <td className="px-6 py-4"><button onClick={() => toggleExpand(rfq.id)} className="text-slate-400 hover:text-slate-700"><Icon name={expandedRfq === rfq.id ? 'chevronUp' : 'chevronDown'} className="w-5 h-5" /></button></td>
                                        <td className="px-6 py-4 whitespace-nowrap text-sm font-medium text-red-700">{rfq.id}</td><td className="px-6 py-4 whitespace-nowrap text-sm text-slate-700">{rfq.customer}</td><td className="px-6 py-4 whitespace-nowrap text-sm text-slate-500">{rfq.model}</td><td className="px-6 py-4 whitespace-nowrap text-sm text-slate-500">{rfq.pm}</td><td className="px-6 py-4 whitespace-nowrap text-sm text-slate-500">{rfq.status}</td><td className="px-6 py-4 whitespace-nowrap text-sm text-slate-500">{rfq.applicationDate}</td>
                                        <td className="px-6 py-4 whitespace-nowrap text-right text-sm font-medium"><button onClick={() => onSelectRfq(rfq)} className="bg-red-700 hover:bg-red-800 text-white font-bold py-2 px-4 rounded-lg transition-colors disabled:bg-slate-300 disabled:cursor-not-allowed" disabled={rfq.status === 'Rejected'}>Create NPDA</button></td>
                                    </tr>
                                    {expandedRfq === rfq.id && ( <tr className="bg-slate-50"><td colSpan="8" className="px-12 py-4"><h4 className="font-semibold text-slate-700">RFQ Cost Summary</h4><div className="mt-2 max-w-md text-sm space-y-1"><CostRow label="Materials Cost" value={rfq.materialsCost} /><CostRow label="Labor Cost" value={rfq.laborCost} /><CostRow label="Overhead" value={rfq.overhead} /><CostRow label="COGS" value={rfq.cogs} /><div className="flex justify-between py-1 font-bold"><span className="text-red-700">Final Quote (ASP):</span><span className="text-red-700">${rfq.asp}</span></div></div></td></tr> )}
                                </React.Fragment>
                            ))}
                        </tbody>
                    </table>
                </div>
            </Card>
        </div>
    );
};

// --- Dashboard 元件 ---
const Dashboard = ({ projects, onSelectProject, onEditProject }) => {
    const getStatusStyle = (status) => { const styles = { 'RFQ': 'bg-sky-100 text-sky-800 border-sky-300', 'NPDA': 'bg-amber-100 text-amber-800 border-amber-300', 'NPA Meeting': 'bg-purple-100 text-purple-800 border-purple-300', 'MP': 'bg-emerald-100 text-emerald-800 border-emerald-300', 'default': 'bg-slate-100 text-slate-800 border-slate-300' }; return styles[status] || styles['default']; };
    return (
        <div className="px-4 sm:px-6 lg:px-8">
            <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                {projects.map(project => (
                    <Card key={project.id} className="p-6 transition-all duration-300 hover:shadow-xl hover:-translate-y-1 flex flex-col">
                        <div className="flex-grow">
                            <div className="flex justify-between items-start"><h3 className="text-xl font-bold text-red-700 mb-1">{project.modelName || 'Unnamed Project'}</h3><span className={`text-xs font-semibold px-3 py-1 rounded-full border ${getStatusStyle(project.status)}`}>{project.status || 'Unknown'}</span></div>
                            <p className="text-slate-600 text-sm">Product ID: {project.productId || 'N/A'}</p><p className="text-slate-500 text-xs mt-1">Source RFQ: {project.rfqId || 'N/A'}</p>
                            <div className="w-full bg-slate-200 rounded-full h-2 my-4"><div className="bg-red-700 h-2 rounded-full" style={{ width: `${project.progress || 0}%` }}></div></div>
                        </div>
                        <div className="flex justify-end space-x-2 border-t border-slate-200 pt-4 mt-4"><button onClick={() => onEditProject(project)} className="text-sm bg-slate-200 hover:bg-slate-300 text-slate-800 font-semibold py-1 px-3 rounded-md transition-colors">Edit</button><button onClick={() => onSelectProject(project)} className="text-sm bg-red-700 hover:bg-red-800 text-white font-semibold py-1 px-3 rounded-md transition-colors">View Report</button></div>
                    </Card>
                ))}
            </div>
        </div>
    );
};

// --- NPDA 表單的初始資料結構 ---
const initialFormData = {
    id: null, modelName: '', productId: '', status: 'NPDA', rfqId: '',
    overview: { 
        application: 'eReader', npdaType: 'Type B', tftSubstrate: 'Glass', tftSubstrateOther: '', 
        moduleStructure: [], specialStructure: 'NA', specialStructureExplanation: '', 
        existingSimilarProduct: '', newProductId: '',
        screenSize: '', displayResolutionH: '', displayResolutionV: '', ppi: '',
        activeAreaH: '', activeAreaV: '', pixelPitchH: '', pixelPitchV: '',
        outlineDimensionW: '', outlineDimensionH: '', outlineDimensionD: '',
        displayType: 'EPD', numberOfGray: '16', wf: '', glassTftBackplane: '', glassThickness: '',
        fpl: 'ACeP1', fplExplanation: '', ps: 'APS195', psExplanation: '',
        fl: '有', cl: 'NA', clExplanation: '', surfaceTreatment: '',
        tftVendor: '', tftExplanation: '', fpc: 'N/A',
        icBonding: 'N/A', icExplanation: '', touchSenser: 'None', touchExplanation: '',
        segmentCount: '', segmentOthers: '',
        reliabilityRequirement: 'Standard', reliabilityRequirementOthers: '',
        safetyRequirement: 'None', safetyRequirementOthers: '',
        envSubstances: [], envSubstancesOthers: '',
        rawMaterialsConsigned: 'No', rawMaterialsExplanation: '',
        ownerSales: '', ownerPd: '', ownerMfg: '', ownerPp: '', ownerNps: '', ownerPur: '',
    },
    customerAnalysis: { 
        customerName: '', customerAttribute: 'Existing', address: '', 
        contactName: '', contactTitle: '', contactPhone: '', contactFax: '',
        position: 'Shared', confidenceToEarnBusiness: 'High Confidence',
        existingCompetitor: 'None', competitorsPrice: '',
        productSubstitution: 'None', substitution: '',
        productFeatures: '', productFeaturesExp: '',
        acceptedQuality: '', acceptedQualityExp: '',
        lowerCost: '', lowerCostExp: '',
        onTimeDelivery: '', onTimeDeliveryExp: '',
        satisfiedService: '', satisfiedServiceExp: '',
        others: '',
        forecast: [], 
    },
    demandAndMilestone: {
        inRoadmap: 'Yes',
        wsDate: '', wsQty: '',
        esDate: '', esQty: '',
        ppDate: '', ppQty: '',
        mp1Date: '', mp1Qty: '',
        additionalRequest: '',
        existingSimilar: '', newEquipment: '',
        newComponent: '', newProcess: '',
        tftGlass: 'Standard', tftGlassExp: '',
        ic: 'Standard', icExp: '',
        fpc: 'Standard', fpcExp: '',
        ps: 'Standard', psExp: '',
        oca: 'Standard', ocaExp: '',
        agFilm: 'Standard', agFilmExp: '',
        lgp: 'Standard', lgpExp: '',
        lb: 'Standard', lbExp: '',
        tp: 'Standard', tpExp: '',
        emr: 'Standard', emrExp: '',
        activeAreaH: '', activeAreaV: '',
        fpl: 'Standard',
        materialsUtilization: {
            fpc: '', dataL: '', dataW: '', dataA: '', dataB: '', dataR: '', dataC: '',
            remarkL: '', remarkW: '', remarkA: '', remarkB: '', remarkR: '', remarkC: '',
            remarkAxR: '', remarkBxC: '', remarkLaxR: '', remarkWbxC: '', remarkRxC: '',
            remarkTFTU: '', remarkOverallU: '',
        },
        riskAssessment: [
            { category: 'Design', item: '', risk: '', actionPlan: '' },
            { category: 'Process', item: '', risk: '', actionPlan: '' },
        ] 
    },
    businessAssessment: {
        materialsCost: 0, asp: 0,
        laborCost: 0, cogs: 0,
        overhead: 0,
        breakevenQty: '',
        newProductInitialization: '',
        committeeReport: '',
        capacityYield: [],
    },
    operation: {
        pm: '',
        newBudgetRequired: 'No',
        budgetDescription: '',
        pmAttachments: '',
        budgetId: '',
        budgetName: '',
        budgetAmount: '',
        remark: '',
    }
};

// --- NPDA 表單元件 (完整版) ---
const NPDAForm = ({ project, rfq, onSave, onCancel }) => {
    const [activeTab, setActiveTab] = useState('overview');
    const [formData, setFormData] = useState(initialFormData);
    const [isRfqModalOpen, setIsRfqModalOpen] = useState(false);

    useEffect(() => {
        let data = JSON.parse(JSON.stringify(initialFormData));
        data.productId = `ED${Math.floor(100000 + Math.random() * 900000)}`;

        if (data.customerAnalysis.forecast.length === 0) {
            const currentYear = new Date().getFullYear();
            for (let i = 0; i < 36; i++) {
                const year = currentYear + Math.floor(i / 12);
                const month = (i % 12) + 1;
                data.customerAnalysis.forecast.push({ year, month, tam: '', sam: '', asp: '' });
            }
        }

        if (data.businessAssessment.capacityYield.length === 0) {
            const currentYear = new Date().getFullYear();
            for (let i = 0; i < 36; i++) {
                const year = currentYear + Math.floor(i / 12);
                const month = (i % 12) + 1;
                data.businessAssessment.capacityYield.push({ year, month, arrayAlloc: '', arrayYield: '', module1Cap: '', module1Yield: '', module2Cap: '', module2Yield: '', remark: '' });
            }
        }
        
        const source = project || rfq;
        if (source) {
            data.modelName = source.model || source.modelName;
            data.rfqId = source.id || source.rfqId;
            if (rfq) {
                data.customerAnalysis.customerName = rfq.customer;
                data.businessAssessment = { ...data.businessAssessment, materialsCost: rfq.materialsCost, laborCost: rfq.laborCost, overhead: rfq.overhead, cogs: rfq.cogs, asp: rfq.asp };
                data.operation.pm = rfq.pm;
            }
            if (project) {
                 // Deep merge for editing
                Object.keys(data).forEach(key => {
                    if (project[key]) {
                        if (typeof data[key] === 'object' && !Array.isArray(data[key]) && data[key] !== null) {
                            data[key] = { ...data[key], ...project[key] };
                        } else {
                            data[key] = project[key];
                        }
                    }
                });
            }
        }
        
        setFormData(data);
    }, [project, rfq]);

    const handleNestedChange = (section, name, value) => { setFormData(prev => ({ ...prev, [section]: { ...(prev[section] || {}), [name]: value } })); };
    
    const handleModuleStructureChange = (component, isChecked) => {
        let currentStructure = formData.overview?.moduleStructure || [];
        if (isChecked) { if (!currentStructure.includes(component)) { handleNestedChange('overview', 'moduleStructure', [...currentStructure, component]); }
        } else { handleNestedChange('overview', 'moduleStructure', currentStructure.filter(c => c !== component)); }
    };
    
    const moveModuleComponent = (index, direction) => {
        let currentStructure = [...(formData.overview?.moduleStructure || [])];
        const newIndex = index + direction;
        if (newIndex >= 0 && newIndex < currentStructure.length) {
            [currentStructure[index], currentStructure[newIndex]] = [currentStructure[newIndex], currentStructure[index]];
            handleNestedChange('overview', 'moduleStructure', currentStructure);
        }
    };
    
    const handleEnvSubstancesChange = (value, isChecked) => {
        let currentEnv = formData.overview?.envSubstances || [];
        if (isChecked) {
            if (!currentEnv.includes(value)) { handleNestedChange('overview', 'envSubstances', [...currentEnv, value]); }
        } else { handleNestedChange('overview', 'envSubstances', currentEnv.filter(item => item !== value)); }
    };

    const handleCustomerForecastChange = (index, field, value) => {
        const updatedForecast = [...formData.customerAnalysis.forecast];
        updatedForecast[index][field] = value;
        handleNestedChange('customerAnalysis', 'forecast', updatedForecast);
    };
    
    const handleCapacityYieldChange = (index, field, value) => {
        const updatedCapacity = [...formData.businessAssessment.capacityYield];
        updatedCapacity[index][field] = value;
        handleNestedChange('businessAssessment', 'capacityYield', updatedCapacity);
    };

    const handleRiskChange = (index, field, value) => {
        const updatedRisks = [...formData.demandAndMilestone.riskAssessment];
        updatedRisks[index][field] = value;
        handleNestedChange('demandAndMilestone', 'riskAssessment', updatedRisks);
    };

    const addRiskRow = () => {
        const newRisk = { category: '', item: '', risk: '', actionPlan: '' };
        handleNestedChange('demandAndMilestone', 'riskAssessment', [...formData.demandAndMilestone.riskAssessment, newRisk]);
    };

    const handleSubmit = (e) => { e.preventDefault(); onSave(formData); };

    const revenue = formData.businessAssessment.asp || 0;
    const grossProfit = revenue - (formData.businessAssessment.cogs || 0);
    const grossProfitPercent = revenue > 0 ? ((grossProfit / revenue) * 100).toFixed(1) + '%' : '0%';

    const TabButton = ({ view, label }) => ( <button type="button" onClick={() => setActiveTab(view)} className={`px-4 py-2 text-sm font-medium rounded-t-lg border-b-2 transition-colors ${activeTab === view ? 'border-red-700 text-red-700' : 'border-transparent text-slate-500 hover:border-slate-300 hover:text-slate-700'}`}>{label}</button> );
    const FormSection = ({ title, children, gridCols = 'md:grid-cols-2' }) => ( <div className="pt-8"><h3 className="text-lg font-semibold mb-4 text-slate-700 border-b border-slate-200 pb-2">{title}</h3><div className={`grid grid-cols-1 ${gridCols} gap-x-6 gap-y-4`}>{children}</div></div> );
    const FormField = ({ label, children, required=false, fromRfq=false }) => ( <div><label className="block text-sm font-medium text-slate-600 mb-1">{label}{required && <span className="text-red-500 ml-1">*</span>}{fromRfq && <span className="text-xs text-red-700 ml-2">[來自 RFQ]</span>}</label>{children}</div> );
    const Input = ({ section, name, className = '', ...props }) => <input name={name} {...props} value={(section ? formData[section]?.[name] : formData[name]) || ''} onChange={(e) => section ? handleNestedChange(section, name, e.target.value) : setFormData(p => ({...p, [name]: e.target.value}))} className={`w-full bg-white border border-slate-300 rounded-md p-2 focus:border-red-700 focus:ring-1 focus:ring-red-700 disabled:bg-slate-100 disabled:text-slate-500 ${className}`} />;
    const Select = ({ section, name, children, ...props }) => <select name={name} {...props} value={formData[section]?.[name] || ''} onChange={(e) => handleNestedChange(section, name, e.target.value)} className="w-full bg-white border border-slate-300 rounded-md p-2 focus:border-red-700 focus:ring-1 focus:ring-red-700">{children}</select>;
    const DisplayField = ({label, value, fromRfq=false}) => <div><label className="block text-sm font-medium text-slate-600 mb-1">{label} {fromRfq && <span className="text-xs text-red-700 ml-2">[來自 RFQ]</span>}</label><div className="w-full bg-slate-100 border border-slate-300 rounded-md p-2 text-slate-800 font-medium">{value || 'N/A'}</div></div>
    const InputWithUnit = ({ unit, section, name, ...props }) => (<div className="relative"><Input section={section} name={name} {...props} className="pr-12" /><div className="pointer-events-none absolute inset-y-0 right-0 flex items-center pr-3"><span className="text-gray-500 sm:text-sm">{unit}</span></div></div>);
    const InputGroupWithUnit = ({ unit, fields }) => (<div className="flex items-center space-x-2"><div className="flex-1"><Input section={fields[0].section} name={fields[0].name} type="number" placeholder="W/H" /></div><span>x</span><div className="flex-1"><Input section={fields[1].section} name={fields[1].name} type="number" placeholder="H/V" /></div>{fields.length > 2 && <span>x</span>}{fields.length > 2 && <div className="flex-1"><Input section={fields[2].section} name={fields[2].name} type="number" placeholder="D" /></div>}<span className="text-gray-500 sm:text-sm pl-2">{unit}</span></div>);
    const RadioGroup = ({ section, name, options }) => (
        <div className="flex items-center space-x-4">
            {options.map(option => (
                <label key={option} className="flex items-center space-x-2">
                    <input type="radio" name={name} value={option} checked={formData[section]?.[name] === option} onChange={e => handleNestedChange(section, name, e.target.value)} className="h-4 w-4 text-red-700 border-gray-300 focus:ring-red-700" />
                    <span>{option}</span>
                </label>
            ))}
        </div>
    );

    if (!formData.overview) return <div className="p-8 text-center">正在載入表單資料...</div>;

    return (
        <div className="px-4 sm:px-6 lg:px-8">
        <Card>
            {formData.rfqId && ( <div className="p-4 bg-red-50 border-b border-red-200 text-red-800 rounded-t-xl">此 NPDA 申請基於 RFQ: <span className="font-bold">{formData.rfqId}</span>. 部分欄位為唯讀。</div> )}
            <form onSubmit={handleSubmit}>
                <div className="p-6">
                     <div className="flex flex-wrap border-b border-slate-200">
                        <TabButton view="overview" label="產品總覽" />
                        <TabButton view="customer" label="客戶分析" />
                        <TabButton view="milestone" label="需求與時程" />
                        <TabButton view="business" label="商業評估" />
                        <TabButton view="operation" label="營運" />
                    </div>
                    <div className="mt-6 max-h-[60vh] overflow-y-auto pr-4">
                       {activeTab === 'overview' && (
                           <>
                            <FormSection gridCols="md:grid-cols-2">
                                <FormField label="應用領域 (Application)" required><Select section="overview" name="application" required>{formOptions.application.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField>
                                <FormField label="NPDA 類型 (NPDA Type)" required><Select section="overview" name="npdaType" required>{formOptions.npdaType.map(o => <option key={o.value} value={o.value}>{o.label}</option>)}</Select></FormField>
                            </FormSection>
                            <FormSection gridCols="md:grid-cols-2">
                                <FormField label="TFT 基板 (TFT Substrate)" required><Select section="overview" name="tftSubstrate" required>{formOptions.tftSubstrate.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField>
                                {formData.overview.tftSubstrate === 'Others' && <FormField label="其他基板說明" required><Input section="overview" name="tftSubstrateOther" type="text" required /></FormField>}
                            </FormSection>
                            <FormSection title="模組結構 (Module Structure)" gridCols="md:grid-cols-2">
                                <div><FormField label="可用元件"><div className="space-y-2 mt-2">{formOptions.moduleStructureComponents.map(comp => (<label key={comp} className="flex items-center space-x-3"><input type="checkbox" checked={formData.overview.moduleStructure?.includes(comp)} onChange={(e) => handleModuleStructureChange(comp, e.target.checked)} className="h-4 w-4 rounded border-gray-300 text-red-700 focus:ring-red-700" /><span className="text-sm text-slate-700">{comp}</span></label>))}</div></FormField></div>
                                <div><FormField label="已選結構 (由上至下排序)">{formData.overview.moduleStructure?.length > 0 ? (<div className="mt-2 border rounded-md p-2 space-y-1 bg-slate-50">{formData.overview.moduleStructure.map((comp, index) => (<div key={index} className="flex items-center justify-between bg-white p-2 border rounded"><span className="font-medium">{comp}</span><div className="space-x-1"><button type="button" onClick={() => moveModuleComponent(index, -1)} disabled={index === 0} className="p-1 rounded-full hover:bg-slate-100 disabled:opacity-30 disabled:cursor-not-allowed"><Icon name="arrowUp" className="w-4 h-4 text-slate-500" /></button><button type="button" onClick={() => moveModuleComponent(index, 1)} disabled={index === formData.overview.moduleStructure.length - 1} className="p-1 rounded-full hover:bg-slate-100 disabled:opacity-30 disabled:cursor-not-allowed"><Icon name="arrowDown" className="w-4 h-4 text-slate-500" /></button></div></div>))}</div>) : <p className="text-sm text-slate-500 mt-2">請從左側勾選元件來建立結構。</p>}</FormField></div>
                            </FormSection>
                            <FormSection gridCols="md:grid-cols-2">
                                 <FormField label="特殊結構 (Special Structure)" required><Select section="overview" name="specialStructure" required>{formOptions.specialStructure.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField>
                                 {formData.overview.specialStructure !== 'NA' && <FormField label="特殊結構說明"><Input section="overview" name="specialStructureExplanation" type="text"/></FormField>}
                            </FormSection>
                             <FormSection gridCols="md:grid-cols-2">
                                <FormField label="既有相似產品 (Existing Similar Product)" required><Input section="overview" name="existingSimilarProduct" type="text" placeholder="輸入產品 ID 或 NA" required/></FormField>
                                <FormField label="新產品 ID / 型號 (New Product ID)" fromRfq={!!rfq}><Input name="modelName" type="text" value={formData.modelName} readOnly={!!rfq} /></FormField>
                             </FormSection>
                             <FormSection title="產品結構說明 (Product Structure Notes)" gridCols="md:grid-cols-4">
                                <div className="md:col-span-2"><FormField label="螢幕尺寸 (Screen Size)"><InputWithUnit unit="Inch" section="overview" name="screenSize" type="number" /></FormField></div>
                                <div className="md:col-span-2"><FormField label="解析度 (Display Resolution)" required><InputGroupWithUnit unit="Pixel" fields={[{section: "overview", name: "displayResolutionH"}, {section: "overview", name: "displayResolutionV"}]} /></FormField></div>
                                <div className="md:col-span-2"><FormField label="PPI"><InputWithUnit unit="PPI" section="overview" name="ppi" type="number" /></FormField></div>
                                <div className="md:col-span-2"><FormField label="有效區域 (Active Area)" required><InputGroupWithUnit unit="mm" fields={[{section: "overview", name: "activeAreaH"}, {section: "overview", name: "activeAreaV"}]} /></FormField></div>
                                <div className="md:col-span-2"><FormField label="像素間距 (Pixel Pitch)"><InputGroupWithUnit unit="mm" fields={[{section: "overview", name: "pixelPitchH"}, {section: "overview", name: "pixelPitchV"}]} /></FormField></div>
                                <div className="md:col-span-2"><FormField label="外觀尺寸 (Outline Dimension)" required><InputGroupWithUnit unit="mm" fields={[{section: "overview", name: "outlineDimensionW"}, {section: "overview", name: "outlineDimensionH"}, {section: "overview", name: "outlineDimensionD"}]} /></FormField></div>
                                <div className="md:col-span-2"><FormField label="顯示類型 (Display Type)" required><Select section="overview" name="displayType">{formOptions.displayType.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div className="md:col-span-2"><FormField label="灰階數 (Number of Gray)"><Input section="overview" name="numberOfGray" type="number" /></FormField></div>
                                <div className="md:col-span-2"><FormField label="Waveform (WF)" required><Input section="overview" name="wf" type="text"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="Glass/TFT/BackPlane" required><Input section="overview" name="glassTftBackplane" type="text"/></FormField></div>
                                <div className="md:col-span-4"><FormField label="玻璃厚度 (Glass Thickness mm)"><InputWithUnit unit="mm" section="overview" name="glassThickness" type="number" /></FormField></div>
                                <div className="md:col-span-2"><FormField label="FPL" required><Select section="overview" name="fpl">{formOptions.fpl.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div className="md:col-span-2"><FormField label="FPL 說明"><Input section="overview" name="fplExplanation" type="text" /></FormField></div>
                                <div className="md:col-span-2"><FormField label="PS" required><Select section="overview" name="ps">{formOptions.ps.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div className="md:col-span-2"><FormField label="PS 說明"><Input section="overview" name="psExplanation" type="text" /></FormField></div>
                                <div className="md:col-span-2"><FormField label="FL" required><Select section="overview" name="fl">{formOptions.fl.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div className="md:col-span-2"><FormField label="CL" required><Select section="overview" name="cl">{formOptions.cl.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div className="md:col-span-4"><FormField label="CL 說明"><Input section="overview" name="clExplanation" type="text" /></FormField></div>
                                <div className="md:col-span-4"><FormField label="表面處理 (Surface Treatment)" required><Input section="overview" name="surfaceTreatment" type="text"/></FormField></div>
                            </FormSection>
                            <FormSection title="關鍵元件規格 (Key Component Details)" gridCols="md:grid-cols-4">
                                <div className="md:col-span-2"><FormField label="TFT Vendor" required><Select section="overview" name="tftVendor">{formOptions.tftVendor.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div className="md:col-span-2"><FormField label="TFT Explanation"><Input section="overview" name="tftExplanation" type="text"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="FPC" required><Select section="overview" name="fpc">{formOptions.fpc.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div className="md:col-span-2"><FormField label="IC Bonding" required><Select section="overview" name="icBonding">{formOptions.icBonding.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div className="md:col-span-2"><FormField label="IC Explanation"><Input section="overview" name="icExplanation" type="text"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="Touch Senser" required><Select section="overview" name="touchSenser">{formOptions.touchSenser.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div className="md:col-span-2"><FormField label="Touch Explanation"><Input section="overview" name="touchExplanation" type="text"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="Segment Count (Segment only)" required><Input section="overview" name="segmentCount" type="number"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="Others"><Input section="overview" name="segmentOthers" type="text"/></FormField></div>
                            </FormSection>
                            <FormSection title="需求 (Requirements)" gridCols="md:grid-cols-2">
                                <div><FormField label="可靠度需求 (Reliability Requirement)" required><Select section="overview" name="reliabilityRequirement">{formOptions.reliabilityRequirement.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div><FormField label="可靠度需求 - 其他"><Input section="overview" name="reliabilityRequirementOthers" type="text"/></FormField></div>
                                <div><FormField label="安規需求 (Safety Requirement)" required><Select section="overview" name="safetyRequirement">{formOptions.safetyRequirement.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div><FormField label="安規需求 - 其他"><Input section="overview" name="safetyRequirementOthers" type="text"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="環保物質資料需求 (Environmental Substances Data Requirement)" required>
                                    <div className="mt-2 grid grid-cols-2 sm:grid-cols-3 gap-2">
                                        {formOptions.envSubstances.map(item => (
                                            <label key={item} className="flex items-center space-x-2"><input type="checkbox" checked={formData.overview.envSubstances.includes(item)} onChange={e => handleEnvSubstancesChange(item, e.target.checked)} className="h-4 w-4 rounded border-gray-300 text-red-700 focus:ring-red-700" /><span>{item}</span></label>
                                        ))}
                                    </div>
                                </FormField></div>
                                <div className="md:col-span-2"><FormField label="環保物質資料需求 - 其他"><Input section="overview" name="envSubstancesOthers" type="text"/></FormField></div>
                            </FormSection>
                            <FormSection title="其他 (Others)" gridCols="md:grid-cols-4">
                                <div className="md:col-span-2"><FormField label="客供料 (Raw Materials/Components Consigned)" required><Select section="overview" name="rawMaterialsConsigned">{formOptions.consigned.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div className="md:col-span-2"><FormField label="說明 (Explanation)"><Input section="overview" name="rawMaterialsExplanation" type="text"/></FormField></div>
                            </FormSection>
                            <FormSection title="權責單位 (Owner)" gridCols="md:grid-cols-4">
                                <FormField label="Sales" required><Input section="overview" name="ownerSales" type="text"/></FormField>
                                <FormField label="PD" required><Input section="overview" name="ownerPd" type="text"/></FormField>
                                <FormField label="MFG" required><Input section="overview" name="ownerMfg" type="text"/></FormField>
                                <FormField label="PP" required><Input section="overview" name="ownerPp" type="text"/></FormField>
                                <FormField label="NPS" required><Input section="overview" name="ownerNps" type="text"/></FormField>
                                <FormField label="PUR" required><Input section="overview" name="ownerPur" type="text"/></FormField>
                            </FormSection>
                           </>
                       )}
                       {activeTab === 'customer' && (
                           <>
                            <FormSection title="客戶基本資料 (Customer Basics)" gridCols="md:grid-cols-2">
                                <FormField label="客戶名稱 (Customer Name)" fromRfq={!!rfq}><Input section="customerAnalysis" name="customerName" type="text" readOnly={!!rfq} /></FormField>
                                <FormField label="客戶屬性 (Customer Attribute)" required><Select section="customerAnalysis" name="customerAttribute">{formOptions.customerAttribute.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField>
                                <div className="md:col-span-2"><FormField label="地址 (Address)" required><Input section="customerAnalysis" name="address" type="text"/></FormField></div>
                                <FormField label="聯絡人姓名 (Contact Name)" required><Input section="customerAnalysis" name="contactName" type="text"/></FormField>
                                <FormField label="職稱 (Contact Title)" required><Input section="customerAnalysis" name="contactTitle" type="text"/></FormField>
                                <FormField label="電話 (Contact Phone)" required><Input section="customerAnalysis" name="contactPhone" type="text"/></FormField>
                                <FormField label="傳真 (Contact Fax)"><Input section="customerAnalysis" name="contactFax" type="text"/></FormField>
                            </FormSection>
                            <FormSection title="競爭評估 (Competition Assessment)" gridCols="md:grid-cols-2">
                                <div><FormField label="競爭態勢 (Position)" required><RadioGroup section="customerAnalysis" name="position" options={formOptions.position} /></FormField></div>
                                <div><FormField label="贏得業務的信心度 (Confidence to Earn The Business)" required><Select section="customerAnalysis" name="confidenceToEarnBusiness">{formOptions.confidenceToEarnBusiness.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div><FormField label="現有競爭者 (Existing Competitor(s))" required><Select section="customerAnalysis" name="existingCompetitor">{formOptions.existingCompetitors.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div><FormField label="競爭者價格 (Competitors Price)"><InputWithUnit unit="USD" section="customerAnalysis" name="competitorsPrice" type="number" /></FormField></div>
                                <div><FormField label="替代產品 (Product Substitution(s))" required><Select section="customerAnalysis" name="productSubstitution">{formOptions.productSubstitutions.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div><FormField label="替代品說明 (Substitution(s))"><Input section="customerAnalysis" name="substitution" type="text"/></FormField></div>
                            </FormSection>
                            <FormSection title="贏得業務的理想客戶標準、權重和期望" gridCols="md:grid-cols-2">
                                <div><FormField label="產品特性 (Product Features)" required><Input section="customerAnalysis" name="productFeatures" type="text"/></FormField></div>
                                <div><FormField label="說明 (Explanation)"><Input section="customerAnalysis" name="productFeaturesExp" type="text"/></FormField></div>
                                <div><FormField label="可接受的品質 (Accepted Quality)" required><Input section="customerAnalysis" name="acceptedQuality" type="text"/></FormField></div>
                                <div><FormField label="說明 (Explanation)"><Input section="customerAnalysis" name="acceptedQualityExp" type="text"/></FormField></div>
                                <div><FormField label="更低的成本 (Lower Cost)" required><Input section="customerAnalysis" name="lowerCost" type="text"/></FormField></div>
                                <div><FormField label="說明 (Explanation)"><Input section="customerAnalysis" name="lowerCostExp" type="text"/></FormField></div>
                                <div><FormField label="準時交貨 (On Time Delivery)" required><Input section="customerAnalysis" name="onTimeDelivery" type="text"/></FormField></div>
                                <div><FormField label="說明 (Explanation)"><Input section="customerAnalysis" name="onTimeDeliveryExp" type="text"/></FormField></div>
                                <div><FormField label="滿意的服務 (Satisfied Service)" required><Input section="customerAnalysis" name="satisfiedService" type="text"/></FormField></div>
                                <div><FormField label="說明 (Explanation)"><Input section="customerAnalysis" name="satisfiedServiceExp" type="text"/></FormField></div>
                            </FormSection>
                            <FormSection title="其他 (Others)" gridCols="md:grid-cols-1">
                                <FormField label="其他說明" required>
                                    <Input section="customerAnalysis" name="others" type="text" />
                                </FormField>
                            </FormSection>
                            <FormSection title="量產後三年預測 (3 Years Forecast after MP)" gridCols="md:grid-cols-1">
                               <p className="text-sm text-slate-500 -mt-2 mb-4">預測應在第一年的第一季和第二年的上半年確定。</p>
                               <div className="overflow-x-auto border border-slate-200 rounded-lg">
                                   <table className="min-w-full text-sm text-center">
                                       <thead className="bg-slate-50">
                                           <tr>
                                               <th className="sticky left-0 bg-slate-50 p-2 border-r">Year</th>
                                               {formData.customerAnalysis.forecast.slice(0,12).map((d,i) => <th key={`y1-${i}`} colSpan={i === 0 ? 12 : 0} className="p-2 border-b">{d.year}</th>)}
                                               {formData.customerAnalysis.forecast.slice(12,24).map((d,i) => <th key={`y2-${i}`} colSpan={i === 0 ? 12 : 0} className="p-2 border-b">{d.year}</th>)}
                                               {formData.customerAnalysis.forecast.slice(24,36).map((d,i) => <th key={`y3-${i}`} colSpan={i === 0 ? 12 : 0} className="p-2 border-b">{d.year}</th>)}
                                           </tr>
                                           <tr>
                                               <th className="sticky left-0 bg-slate-50 p-2 border-r">Month</th>
                                               {formData.customerAnalysis.forecast.map((d, i) => <th key={`m-${i}`} className="font-normal p-2 border-t">{d.month}</th>)}
                                           </tr>
                                       </thead>
                                       <tbody className="bg-white">
                                           <tr>
                                               <td className="sticky left-0 bg-white p-2 border-r text-left text-xs font-medium">TAM_Total Available Market Volume (pc)</td>
                                               {formData.customerAnalysis.forecast.map((d, i) => (
                                                   <td key={`tam-${i}`} className="p-1 border-t"><input type="number" value={d.tam} onChange={e => handleCustomerForecastChange(i, 'tam', e.target.value)} className="w-20 text-center p-1 rounded border-slate-200 focus:ring-red-700 focus:border-red-700"/></td>
                                               ))}
                                           </tr>
                                           <tr>
                                               <td className="sticky left-0 bg-white p-2 border-r text-left text-xs font-medium">SAM_Sales Available Market Volume (pc)</td>
                                               {formData.customerAnalysis.forecast.map((d, i) => (
                                                   <td key={`sam-${i}`} className="p-1 border-t"><input type="number" value={d.sam} onChange={e => handleCustomerForecastChange(i, 'sam', e.target.value)} className="w-20 text-center p-1 rounded border-slate-200 focus:ring-red-700 focus:border-red-700"/></td>
                                               ))}
                                           </tr>
                                           <tr>
                                               <td className="sticky left-0 bg-white p-2 border-r text-left text-xs font-medium">ASP_Average Selling Price (USD/pc)</td>
                                               {formData.customerAnalysis.forecast.map((d, i) => (
                                                   <td key={`asp-${i}`} className="p-1 border-t"><input type="number" value={d.asp} onChange={e => handleCustomerForecastChange(i, 'asp', e.target.value)} className="w-20 text-center p-1 rounded border-slate-200 focus:ring-red-700 focus:border-red-700"/></td>
                                               ))}
                                           </tr>
                                       </tbody>
                                   </table>
                               </div>
                            </FormSection>
                           </>
                       )}
                       {activeTab === 'milestone' && (
                           <>
                            <FormSection title="產品里程碑 (Product Milestones)" gridCols="md:grid-cols-4">
                                <div className="md:col-span-4"><FormField label="產品是否包含在產品路線圖中?" required><Select section="demandAndMilestone" name="inRoadmap">{formOptions.yesNo.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                                <div className="md:col-span-2"><FormField label="WS 產出日期" required><Input section="demandAndMilestone" name="wsDate" type="date"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="WS 樣品產出數量" required><InputWithUnit unit="pc" section="demandAndMilestone" name="wsQty" type="number"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="ES 產出日期" required><Input section="demandAndMilestone" name="esDate" type="date"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="ES 樣品產出數量" required><InputWithUnit unit="pc" section="demandAndMilestone" name="esQty" type="number"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="PP 產出日期" required><Input section="demandAndMilestone" name="ppDate" type="date"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="PP 樣品產出數量" required><InputWithUnit unit="pc" section="demandAndMilestone" name="ppQty" type="number"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="第一次量產產出日期" required><Input section="demandAndMilestone" name="mp1Date" type="date"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="第一次量產產出數量" required><InputWithUnit unit="pc" section="demandAndMilestone" name="mp1Qty" type="number"/></FormField></div>
                                <div className="md:col-span-4"><FormField label="額外需求"><Input section="demandAndMilestone" name="additionalRequest" type="text"/></FormField></div>
                            </FormSection>
                            <FormSection title="開發可行性評估" gridCols="md:grid-cols-2">
                                <FormField label="現有最相似產品" required><Input section="demandAndMilestone" name="existingSimilar" type="text"/></FormField>
                                <FormField label="新設備/治具/工具" required><Input section="demandAndMilestone" name="newEquipment" type="text"/></FormField>
                                <FormField label="新元件" required><Input section="demandAndMilestone" name="newComponent" type="text"/></FormField>
                                <FormField label="新製程" required><Input section="demandAndMilestone" name="newProcess" type="text"/></FormField>
                            </FormSection>
                            <FormSection title="材料是否為標準品?" gridCols="md:grid-cols-2">
                                <MaterialStandardField name="tftGlass" label="TFT/Glass" />
                                <MaterialStandardField name="ic" label="IC" />
                                <MaterialStandardField name="fpc" label="FPC" />
                                <MaterialStandardField name="ps" label="PS" />
                                <MaterialStandardField name="oca" label="OCA" />
                                <MaterialStandardField name="agFilm" label="AG Film" />
                                <MaterialStandardField name="lgp" label="LGP" />
                                <MaterialStandardField name="lb" label="L/B" />
                                <MaterialStandardField name="tp" label="TP" />
                                <MaterialStandardField name="emr" label="EMR" />
                                <div><FormField label="有效區域-高 (mm)" required><Input section="demandAndMilestone" name="activeAreaH" type="number"/></FormField></div>
                                <div><FormField label="有效區域-寬 (mm)" required><Input section="demandAndMilestone" name="activeAreaV" type="number"/></FormField></div>
                                <div className="md:col-span-2"><FormField label="FPL" required><Select section="demandAndMilestone" name="fpl">{formOptions.materialStandard.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                            </FormSection>
                            <FormSection title="材料利用率" gridCols="md:grid-cols-1">
                                <FormField label="FPC(%)" required><InputWithUnit unit="%" section="demandAndMilestone" name="materialsUtilization.fpc" type="number"/></FormField>
                                <div className="border rounded-lg overflow-hidden mt-4">
                                    <div className="grid grid-cols-10 bg-slate-50 font-semibold text-sm text-center border-b">
                                        <div className="col-span-3 p-2">項目</div>
                                        <div className="col-span-2 p-2 border-l">公式</div>
                                        <div className="col-span-2 p-2 border-l">數據</div>
                                        <div className="col-span-3 p-2 border-l">備註</div>
                                    </div>
                                    <UtilTableRow label="TFT Fab" name="TFT Fab" formula="" dataName="dataTFTFab" remarkName="remarkTFTFab" isTitle />
                                    <UtilTableRow label="Usable Substrate Length (mm)" formula="L" dataName="dataL" remarkName="remarkL" />
                                    <UtilTableRow label="Usable Substrate Width (mm)" formula="W" dataName="dataW" remarkName="remarkW" />
                                    <UtilTableRow label="TFT Length (mm)" formula="a" dataName="dataA" remarkName="remarkA" />
                                    <UtilTableRow label="TFT Width (mm)" formula="b" dataName="dataB" remarkName="remarkB" />
                                    <UtilTableRow label="No. of TFT Rows" formula="R" dataName="dataR" remarkName="remarkR" />
                                    <UtilTableRow label="No. of TFT Columns" formula="C" dataName="dataC" remarkName="remarkC" />
                                    <UtilTableRow label="TFT Length x Rows (mm)" formula="a x R" isCalculated remarkName="remarkAxR" />
                                    <UtilTableRow label="TFT Width x Columns (mm)" formula="b x C" isCalculated remarkName="remarkBxC" />
                                    <UtilTableRow label="Substrate Length Remain (mm)" formula="L - (a x R)" isCalculated remarkName="remarkLaxR" />
                                    <UtilTableRow label="Substrate Width Remain (mm)" formula="W - (b x C)" isCalculated remarkName="remarkWbxC" />
                                    <UtilTableRow label="Total Number of TFT cuts" formula="R x C" isCalculated remarkName="remarkRxC" />
                                    <UtilTableRow label="TFT Utilization" formula="(a x b x R x C) / (L x W)" isCalculated remarkName="remarkTFTU" />
                                    <UtilTableRow label="Overall TFT Utilization" formula="[(a x b x R x C) + (d x e x f)] / (L x W)" isCalculated remarkName="remarkOverallU" />
                                </div>
                            </FormSection>
                            <FormSection title="風險評估" gridCols="md:grid-cols-1">
                                <div className="border rounded-lg overflow-hidden">
                                     <div className="grid grid-cols-12 bg-slate-50 font-semibold text-sm text-center border-b">
                                        <div className="col-span-2 p-2">類別</div>
                                        <div className="col-span-3 p-2 border-l">項目</div>
                                        <div className="col-span-3 p-2 border-l">風險</div>
                                        <div className="col-span-4 p-2 border-l">行動計畫</div>
                                    </div>
                                    <div className="divide-y">
                                        {formData.demandAndMilestone.riskAssessment.map((risk, index) => (
                                            <div key={index} className="grid grid-cols-12 text-sm">
                                                <div className={`col-span-2 p-1 ${(risk.category === 'Design' && 'bg-red-100') || (risk.category === 'Process' && 'bg-red-200') || 'bg-slate-100'}`}>
                                                   <Input value={risk.category} onChange={e => handleRiskChange(index, 'category', e.target.value)} className="bg-transparent border-0" />
                                                </div>
                                                <div className="col-span-3 p-1 border-l"><Input value={risk.item} onChange={e => handleRiskChange(index, 'item', e.target.value)} /></div>
                                                <div className="col-span-3 p-1 border-l"><Input value={risk.risk} onChange={e => handleRiskChange(index, 'risk', e.target.value)} /></div>
                                                <div className="col-span-4 p-1 border-l"><Input value={risk.actionPlan} onChange={e => handleRiskChange(index, 'actionPlan', e.target.value)} /></div>
                                            </div>
                                        ))}
                                    </div>
                                </div>
                                <div className="flex justify-end mt-2">
                                    <button type="button" onClick={addRiskRow} className="text-sm bg-slate-200 hover:bg-slate-300 text-slate-800 font-semibold py-1 px-3 rounded-md transition-colors">新增風險項目</button>
                                </div>
                            </FormSection>
                           </>
                       )}
                       {activeTab === 'business' && (
                           <>
                            <FormSection title="成本與收益分析" gridCols="md:grid-cols-4">
                               <DisplayField label="材料成本 (USD/pc)" value={formData.businessAssessment.materialsCost} fromRfq />
                               <DisplayField label="平均售價 (ASP) (USD/pc)" value={formData.businessAssessment.asp} fromRfq />
                               <DisplayField label="人工成本 (USD/pc)" value={formData.businessAssessment.laborCost} fromRfq />
                               <DisplayField label="銷貨成本 (COGS) (USD/pc)" value={formData.businessAssessment.cogs} fromRfq />
                               <DisplayField label="間接費用 (USD/pc)" value={formData.businessAssessment.overhead} fromRfq />
                               <DisplayField label="收益 (Revenue) (USD)" value={revenue} />
                               <DisplayField label="毛利 (Gross Profit) (USD)" value={grossProfit.toFixed(2)} />
                               <DisplayField label="毛利率 (Gross Profit %)" value={grossProfitPercent} />
                               <div className="md:col-span-4 flex items-end">
                                   <button type="button" onClick={() => setIsRfqModalOpen(true)} className="bg-slate-200 hover:bg-slate-300 text-slate-800 font-bold py-2 px-4 rounded-lg transition-colors">檢視 RFQ Cost Table</button>
                               </div>
                            </FormSection>
                            <FormSection title="產能與良率預估" gridCols="md:grid-cols-1">
                               <div className="overflow-x-auto border border-slate-200 rounded-lg">
                                   <table className="min-w-full text-sm text-center">
                                       <thead className="bg-slate-50 sticky top-0">
                                            <tr>
                                                <th className="p-2 border-b">Year</th>
                                                <th className="p-2 border-b">Month</th>
                                                <th className="p-2 border-b">SAM (pc)</th>
                                                <th className="p-2 border-b">Array Capacity (pc)</th>
                                                <th className="p-2 border-b">Array Yield (%)</th>
                                                <th className="p-2 border-b">Module1 Capacity (pc)</th>
                                                <th className="p-2 border-b">Module1 Yield (%)</th>
                                                <th className="p-2 border-b">Module2 Capacity (pc)</th>
                                                <th className="p-2 border-b">Module2 Yield (%)</th>
                                                <th className="p-2 border-b">編輯</th>
                                            </tr>
                                       </thead>
                                       <tbody className="bg-white">
                                            {formData.businessAssessment.capacityYield.map((d, i) => (
                                                <tr key={i} className="border-t">
                                                    <td className="p-2">{d.year}</td>
                                                    <td className="p-2">{d.month}</td>
                                                    <td className="p-2 bg-slate-50">{formData.customerAnalysis.forecast[i]?.sam || 'N/A'}</td>
                                                    <td className="p-1"><Input value={d.arrayAlloc} onChange={e => handleCapacityYieldChange(i, 'arrayAlloc', e.target.value)} type="number" /></td>
                                                    <td className="p-1"><Input value={d.arrayYield} onChange={e => handleCapacityYieldChange(i, 'arrayYield', e.target.value)} type="number" /></td>
                                                    <td className="p-1"><Input value={d.module1Cap} onChange={e => handleCapacityYieldChange(i, 'module1Cap', e.target.value)} type="number" /></td>
                                                    <td className="p-1"><Input value={d.module1Yield} onChange={e => handleCapacityYieldChange(i, 'module1Yield', e.target.value)} type="number" /></td>
                                                    <td className="p-1"><Input value={d.module2Cap} onChange={e => handleCapacityYieldChange(i, 'module2Cap', e.target.value)} type="number" /></td>
                                                    <td className="p-1"><Input value={d.module2Yield} onChange={e => handleCapacityYieldChange(i, 'module2Yield', e.target.value)} type="number" /></td>
                                                    <td className="p-1"><Input value={d.remark} onChange={e => handleCapacityYieldChange(i, 'remark', e.target.value)} /></td>
                                                </tr>
                                            ))}
                                       </tbody>
                                   </table>
                               </div>
                            </FormSection>
                             <FormSection title="其他評估" gridCols="md:grid-cols-2">
                                <FormField label="損益平衡數量" required><Input section="businessAssessment" name="breakevenQty" type="number"/></FormField>
                                <FormField label="新產品導入" required><Input section="businessAssessment" name="newProductInitialization" /></FormField>
                                <div className="md:col-span-2"><FormField label="委員會報告" required><Input section="businessAssessment" name="committeeReport" /></FormField></div>
                            </FormSection>
                           </>
                       )}
                       {activeTab === 'operation' && (
                           <>
                            <FormSection title="營運資訊" gridCols="md:grid-cols-2">
                                <DisplayField label="PM" value={formData.operation.pm} fromRfq />
                                <FormField label="需要新預算?" required><Select section="operation" name="newBudgetRequired">{formOptions.yesNo.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField>
                                <div className="md:col-span-2"><FormField label="預算說明" required><Input section="operation" name="budgetDescription"/></FormField></div>
                                <FormField label="PM 附件" required><Input section="operation" name="pmAttachments"/></FormField>
                                <FormField label="預算 ID" required><Input section="operation" name="budgetId"/></FormField>
                                <FormField label="預算名稱" required><Input section="operation" name="budgetName"/></FormField>
                                <FormField label="預算金額 (NTD)" required><Input section="operation" name="budgetAmount" type="number"/></FormField>
                                <DisplayField label="新產品 ID" value={formData.productId} />
                                <div className="md:col-span-2"><FormField label="備註"><Input section="operation" name="remark"/></FormField></div>
                            </FormSection>
                           </>
                       )}
                    </div>
                </div>
                <div className="flex justify-end space-x-4 p-4 bg-slate-50 border-t border-slate-200 rounded-b-xl"><button type="button" onClick={onCancel} className="bg-white hover:bg-slate-100 text-slate-700 font-bold py-2 px-6 rounded-lg border border-slate-300 transition-colors">取消</button><button type="submit" className="bg-red-700 hover:bg-red-800 text-white font-bold py-2 px-6 rounded-lg transition-colors">儲存</button></div>
            </form>
        </Card>
        {isRfqModalOpen && <RfqCostModal rfq={rfq || project} onClose={() => setIsRfqModalOpen(false)} />}
        </div>
    );

    function MaterialStandardField({ name, label }) {
        return (
            <>
                <div><FormField label={label} required><Select section="demandAndMilestone" name={name}>{formOptions.materialStandard.map(o => <option key={o} value={o}>{o}</option>)}</Select></FormField></div>
                <div><FormField label="說明"><Input section="demandAndMilestone" name={`${name}Exp`} type="text"/></FormField></div>
            </>
        );
    }
    
    function UtilTableRow({ label, formula, dataName, remarkName, isTitle = false, isCalculated = false }) {
        const handleUtilChange = (field, value) => {
            const updatedUtil = { ...formData.demandAndMilestone.materialsUtilization, [field]: value };
            handleNestedChange('demandAndMilestone', 'materialsUtilization', updatedUtil);
        }
        return (
             <div className={`grid grid-cols-10 text-sm border-t ${isTitle ? 'bg-red-100 font-semibold' : ''}`}>
                <div className="col-span-3 p-2">{label}</div>
                <div className="col-span-2 p-2 border-l text-center">{formula}</div>
                <div className="col-span-2 p-1 border-l">
                    {!isCalculated && <Input value={formData.demandAndMilestone.materialsUtilization[dataName] || ''} onChange={e => handleUtilChange(dataName, e.target.value)} className="text-center"/>}
                </div>
                <div className="col-span-3 p-1 border-l">
                    <Input value={formData.demandAndMilestone.materialsUtilization[remarkName] || ''} onChange={e => handleUtilChange(remarkName, e.target.value)} />
                </div>
            </div>
        );
    }
};

// --- RFQ 成本彈出視窗元件 ---
const RfqCostModal = ({ rfq, onClose }) => {
    if (!rfq) return null;
    const costData = {
        materialsCost: rfq.materialsCost || rfq.businessAssessment?.materialsCost || 0,
        laborCost: rfq.laborCost || rfq.businessAssessment?.laborCost || 0,
        overhead: rfq.overhead || rfq.businessAssessment?.overhead || 0,
        cogs: rfq.cogs || rfq.businessAssessment?.cogs || 0,
        asp: rfq.asp || rfq.businessAssessment?.asp || 0,
        id: rfq.id || rfq.rfqId,
    }
    return (
        <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
            <div className="bg-white rounded-xl shadow-2xl p-6 w-full max-w-md">
                <div className="flex justify-between items-center mb-4">
                    <h3 className="text-xl font-bold text-slate-800">RFQ 成本明細 ({costData.id})</h3>
                    <button onClick={onClose} className="text-slate-400 hover:text-slate-700">&times;</button>
                </div>
                <div className="space-y-2 text-sm">
                    <div className="flex justify-between py-2 border-b"><span className="text-slate-500">材料成本:</span><span className="font-medium">${costData.materialsCost}</span></div>
                    <div className="flex justify-between py-2 border-b"><span className="text-slate-500">人工成本:</span><span className="font-medium">${costData.laborCost}</span></div>
                    <div className="flex justify-between py-2 border-b"><span className="text-slate-500">間接費用:</span><span className="font-medium">${costData.overhead}</span></div>
                    <div className="flex justify-between py-2 border-b bg-slate-50 font-semibold"><span className="text-slate-700">銷貨成本 (COGS):</span><span className="text-slate-900">${costData.cogs}</span></div>
                    <div className="flex justify-between py-2 border-b bg-red-50 font-bold"><span className="text-red-700">平均售價 (ASP):</span><span className="text-red-700">${costData.asp}</span></div>
                </div>
                <div className="mt-6 flex justify-end">
                    <button onClick={onClose} className="bg-red-700 hover:bg-red-800 text-white font-bold py-2 px-6 rounded-lg transition-colors">關閉</button>
                </div>
            </div>
        </div>
    );
};

// --- 時程追蹤 (表格) 元件 ---
const ScheduleTracking = ({ projects }) => {
    return (
        <div className="px-4 sm:px-6 lg:px-8">
            <Card>
                <div className="overflow-x-auto">
                    <table className="min-w-full divide-y divide-slate-200">
                        <thead className="bg-slate-50">
                            <tr>
                                <th className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Project Name</th>
                                <th className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">WS Date</th>
                                <th className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">ES Date</th>
                                <th className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">PP Date</th>
                                <th className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">MP Date</th>
                            </tr>
                        </thead>
                        <tbody className="bg-white divide-y divide-slate-200">
                            {projects.map(project => (
                                <tr key={project.id} className="hover:bg-slate-50">
                                    <td className="px-6 py-4 whitespace-nowrap text-sm font-medium text-red-700">{project.modelName}</td>
                                    <td className="px-6 py-4 whitespace-nowrap text-sm text-slate-500">{project.milestones?.ws || 'N/A'}</td>
                                    <td className="px-6 py-4 whitespace-nowrap text-sm text-slate-500">{project.milestones?.es || 'N/A'}</td>
                                    <td className="px-6 py-4 whitespace-nowrap text-sm text-slate-500">{project.milestones?.pp || 'N/A'}</td>
                                    <td className="px-6 py-4 whitespace-nowrap text-sm text-slate-500">{project.milestones?.mp || 'N/A'}</td>
                                </tr>
                            ))}
                        </tbody>
                    </table>
                </div>
            </Card>
        </div>
    );
};


// --- NPA 報告元件 ---
const NPAReport = ({ project, onBack }) => {
    const [page, setPage] = useState('summary');
    
    if (!project) {
        return (
            <div className="px-4 sm:px-6 lg:px-8">
                <Card><div className="p-8 text-center"><h3 className="text-xl font-semibold text-slate-800">NPA Report</h3><p className="mt-2 text-slate-500">請先從儀表板選擇一個專案來檢視報告。</p><button onClick={onBack} className="mt-4 bg-slate-200 hover:bg-slate-300 text-slate-800 font-semibold py-1 px-3 rounded-md transition-colors">返回</button></div></Card>
            </div>
        );
    }
    
    const grossMargin = project.businessAssessment?.asp > 0 ? (((project.businessAssessment.asp - project.businessAssessment.cogs) / project.businessAssessment.asp) * 100).toFixed(1) + '%' : '0%';

    const ReportPage = ({ title, children }) => <div className="p-6">{children}</div>;
    const Section = ({ title, children, className }) => <div className={`mt-6 ${className}`}><h4 className="font-bold text-red-700 border-b-2 border-red-200 pb-1 mb-2">{title}</h4>{children}</div>;
    const Field = ({ label, value }) => <div className="text-sm py-1"><span className="font-semibold text-slate-600 w-32 inline-block">{label}:</span><span>{value || 'N/A'}</span></div>;

    const renderPage = () => {
        switch(page) {
            case 'summary':
                return <ReportPage title="Summary">
                    <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <Section title="基本資訊">
                                <Field label="Application" value={project.overview?.application} />
                                <Field label="Customer" value={project.customerAnalysis?.customerName} />
                                <Field label="Product Features" value={project.customerAnalysis?.productFeatures} />
                                <Field label="Design Highlight" value={project.overview?.specialStructureExplanation} />
                            </Section>
                             <Section title="規格">
                                <Field label="FPL" value={project.overview?.fpl} />
                                <Field label="TFT Fab" value={project.overview?.tftVendor} />
                                <Field label="Module Fab" value="E Ink" />
                            </Section>
                        </div>
                        <div>
                            <Section title="商業評估">
                                <Field label="Product Cost (USD)" value={project.businessAssessment?.cogs} />
                                <Field label="Gross Margin (%)" value={grossMargin} />
                                <Field label="Budget Plan (NTD)" value={project.operation?.budgetAmount} />
                                <Field label="Payback Q'ty (Pcs)" value={project.businessAssessment?.breakevenQty} />
                            </Section>
                            <Section title="時程">
                                <Field label="WS" value={project.demandAndMilestone?.wsDate} />
                                <Field label="ES" value={project.demandAndMilestone?.esDate} />
                                <Field label="PP" value={project.demandAndMilestone?.ppDate} />
                                <Field label="MP" value={project.demandAndMilestone?.mp1Date} />
                            </Section>
                        </div>
                    </div>
                     <Section title="主要風險">
                        <ul className="list-disc pl-5 text-sm">
                        {project.demandAndMilestone?.riskAssessment?.map((risk, i) => (
                            <li key={i}>{risk.risk}</li>
                        ))}
                        </ul>
                    </Section>
                </ReportPage>;
            case 'specs':
                 return <ReportPage title="Product Specifications">
                    <Section title="產品規格">
                         <div className="grid grid-cols-1 md:grid-cols-2 gap-x-6">
                            <Field label="Screen Size" value={`${project.overview?.screenSize}"`} />
                            <Field label="Display Resolution" value={`${project.overview?.displayResolutionH} x ${project.overview?.displayResolutionV} px`} />
                            <Field label="Active Area" value={`${project.overview?.activeAreaH} x ${project.overview?.activeAreaV} mm`} />
                            <Field label="Pixel Pitch" value={`${project.overview?.pixelPitchH} x ${project.overview?.pixelPitchV} mm`} />
                            <Field label="Outline Dimension" value={`${project.overview?.outlineDimensionW} x ${project.overview?.outlineDimensionH} x ${project.overview?.outlineDimensionD} mm`} />
                            <Field label="Number of Grey" value={project.overview?.numberOfGray} />
                            <Field label="WF" value={project.overview?.wf} />
                            <Field label="Glass/TFT/BackPlane" value={project.overview?.glassTftBackplane} />
                            <Field label="FPL" value={project.overview?.fpl} />
                            <Field label="PS" value={project.overview?.ps} />
                            <Field label="FL" value={project.overview?.fl} />
                            <Field label="CL" value={project.overview?.cl} />
                            <Field label="Surface Treatment" value={project.overview?.surfaceTreatment} />
                        </div>
                    </Section>
                </ReportPage>;
            case 'structure':
                 return <ReportPage title="Product Structure">
                    <Section title="產品結構 (由上至下)">
                        <ol className="list-decimal list-inside bg-slate-50 p-4 rounded-md">
                            {project.overview?.moduleStructure?.map(item => <li key={item}>{item}</li>)}
                        </ol>
                    </Section>
                     <Section title="TFT 利用率">
                        <Field label="TFT Utilization" value={project.demandAndMilestone?.materialsUtilization.remarkTFTU} />
                        <Field label="Overall TFT Utilization" value={project.demandAndMilestone?.materialsUtilization.remarkOverallU} />
                    </Section>
                </ReportPage>;
            case 'components':
                 return <ReportPage title="Key Components">
                     <Section title="關鍵元件列表">
                        <table className="w-full text-sm text-left">
                            <thead className="border-b-2"><tr><th className="py-2">Component</th><th>Key Spec.</th><th>1st Source</th></tr></thead>
                            <tbody>
                                <tr className="border-b"><td className="py-2">FPL</td><td>{project.overview?.fpl}</td><td>E Ink</td></tr>
                                <tr className="border-b"><td className="py-2">PS</td><td>{project.overview?.ps}</td><td>E Ink</td></tr>
                                <tr className="border-b"><td className="py-2">TFT</td><td>{project.overview?.glassTftBackplane}</td><td>{project.overview?.tftVendor}</td></tr>
                                <tr className="border-b"><td className="py-2">IC</td><td>-</td><td>{project.demandAndMilestone?.ic}</td></tr>
                                <tr className="border-b"><td className="py-2">FPC</td><td>-</td><td>{project.demandAndMilestone?.fpc}</td></tr>
                                <tr className="border-b"><td className="py-2">TP</td><td>-</td><td>{project.demandAndMilestone?.tp}</td></tr>
                            </tbody>
                        </table>
                     </Section>
                 </ReportPage>;
            case 'schedule':
                 return <ReportPage title="Development Schedule">
                    <Section title="樣品時程與數量">
                        <table className="w-full text-sm text-left">
                            <thead className="border-b-2"><tr><th className="py-2">Sample</th><th>Date</th><th>Quantity (pcs)</th></tr></thead>
                            <tbody>
                                <tr className="border-b"><td className="py-2 font-semibold">WS</td><td>{project.demandAndMilestone?.wsDate}</td><td>{project.demandAndMilestone?.wsQty}</td></tr>
                                <tr className="border-b"><td className="py-2 font-semibold">ES</td><td>{project.demandAndMilestone?.esDate}</td><td>{project.demandAndMilestone?.esQty}</td></tr>
                                <tr className="border-b"><td className="py-2 font-semibold">PP</td><td>{project.demandAndMilestone?.ppDate}</td><td>{project.demandAndMilestone?.ppQty}</td></tr>
                            </tbody>
                        </table>
                    </Section>
                 </ReportPage>;
             case 'risk':
                 return <ReportPage title="Risk Assessment">
                    <Section title="風險評估">
                         <table className="w-full text-sm text-left">
                            <thead className="border-b-2"><tr><th className="py-2">Category</th><th>Item</th><th>Risk</th><th>Action Plan</th></tr></thead>
                            <tbody>
                            {project.demandAndMilestone?.riskAssessment?.map((risk, i) => (
                                <tr className="border-b" key={i}>
                                    <td className="py-2 pr-2">{risk.category}</td>
                                    <td className="py-2 pr-2">{risk.item}</td>
                                    <td className="py-2 pr-2">{risk.risk}</td>
                                    <td className="py-2 pr-2">{risk.actionPlan}</td>
                                </tr>
                            ))}
                            </tbody>
                        </table>
                    </Section>
                 </ReportPage>;
             case 'budget':
                 return <ReportPage title="Budget & Cost">
                     <Section title="預算規劃">
                        <Field label="預算金額 (NTD)" value={project.operation?.budgetAmount} />
                        <Field label="預算名稱" value={project.operation?.budgetName} />
                        <Field label="預算說明" value={project.operation?.budgetDescription} />
                    </Section>
                     <Section title="成本分析">
                        <Field label="銷貨成本 (COGS)" value={project.businessAssessment?.cogs} />
                        <Field label="平均售價 (ASP)" value={project.businessAssessment?.asp} />
                        <Field label="毛利率 (Gross Margin)" value={grossMargin} />
                    </Section>
                 </ReportPage>;
            default: return <ReportPage title="Summary">...</ReportPage>;
        }
    }
    
    const ReportNavItem = ({ pageName, label }) => (
        <button onClick={() => setPage(pageName)} className={`w-full text-left px-3 py-2 text-sm rounded-md ${page === pageName ? 'bg-red-100 text-red-700 font-bold' : 'hover:bg-slate-100'}`}>
            {label}
        </button>
    );

    return (
        <div className="px-4 sm:px-6 lg:px-8">
            <Card>
                <div className="p-4 border-b flex justify-between items-center">
                    <h2 className="text-xl font-bold text-red-700">NPA Report: {project.modelName}</h2>
                    <button onClick={onBack} className="text-sm bg-slate-200 hover:bg-slate-300 text-slate-800 font-semibold py-1 px-3 rounded-md transition-colors">返回 Dashboard</button>
                </div>
                <div className="flex">
                    <aside className="w-56 border-r p-4">
                        <nav className="space-y-1">
                           <ReportNavItem pageName="summary" label="Summary Table" />
                           <ReportNavItem pageName="specs" label="Product Specifications" />
                           <ReportNavItem pageName="structure" label="Product Structure" />
                           <ReportNavItem pageName="components" label="Key Components" />
                           <ReportNavItem pageName="schedule" label="Development Schedule" />
                           <ReportNavItem pageName="risk" label="Risk Assessment" />
                           <ReportNavItem pageName="budget" label="Budget & Cost" />
                        </nav>
                    </aside>
                    <main className="flex-1">
                        {renderPage()}
                    </main>
                </div>
            </Card>
        </div>
    );
};

