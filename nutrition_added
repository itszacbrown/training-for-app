import { useState } from 'react';
import { X, Check, Calendar, Clock, AlertCircle, Award, User, ArrowRight, ChevronRight, ChevronLeft, Edit, Save, Plus } from 'lucide-react';

export default function TrainReadyApp() {
  // App states
  const [currentScreen, setCurrentScreen] = useState('onboarding');
  const [userName, setUserName] = useState('');
  const [eventName, setEventName] = useState('');
  const [eventDate, setEventDate] = useState('');
  const [daysLeft, setDaysLeft] = useState(42);
  const [currentPhase, setCurrentPhase] = useState(2);
  const [currentDay, setCurrentDay] = useState('Monday');
  const [completedWorkouts, setCompletedWorkouts] = useState({});
  const [showPhaseInfo, setShowPhaseInfo] = useState(false);
  
  // Edit mode states
  const [editMode, setEditMode] = useState(false);
  const [editingItemType, setEditingItemType] = useState(null); // 'workout' or 'meal'
  const [editingItemIndex, setEditingItemIndex] = useState(null);
  const [editFormData, setEditFormData] = useState({});
  const [isNewItem, setIsNewItem] = useState(false);
  
  // Nutrition targets
  const [nutritionTargets, setNutritionTargets] = useState({
    calories: 2000,
    protein: 150,
    carbs: 200,
    fat: 65
  });
  
  // Nutrition setup state
  const [showNutritionSetup, setShowNutritionSetup] = useState(false);
  const [nutritionSetupData, setNutritionSetupData] = useState({
    calories: 2000,
    protein: 150,
    carbs: 200,
    fat: 65
  });

  // Training data state - moved to state so it can be edited
  const [trainingData, setTrainingData] = useState({
    Monday: {
      workout: [
        { name: 'Dumbbell Bench Press', sets: 4, reps: 10, completed: false },
        { name: 'Front Squats with Dumbbells', sets: 4, reps: 12, completed: false },
        { name: 'Bent Over Rows', sets: 4, reps: 10, completed: false },
        { name: 'Kettlebell Swings', sets: 4, reps: 15, completed: false },
        { name: 'Plank', sets: 3, duration: '60s', completed: false }
      ],
      meals: [
        { time: '8 AM', name: 'Greek yogurt with berries + protein + toast', calories: 450, protein: 30, carbs: 45, fat: 12, completed: false },
        { time: '10 AM', name: '2 boiled eggs', calories: 140, protein: 12, carbs: 0, fat: 10, completed: false },
        { time: '12:30 PM', name: 'Grilled chicken breast with quinoa & spinach', calories: 420, protein: 35, carbs: 40, fat: 8, completed: false },
        { time: '3 PM', name: 'Chicken sausage with mustard', calories: 180, protein: 15, carbs: 2, fat: 12, completed: false },
        { time: '6 PM', name: 'Baked salmon with asparagus & sweet potato', calories: 450, protein: 40, carbs: 30, fat: 15, completed: false },
        { time: 'Post-Workout', name: 'Protein shake + creatine', calories: 150, protein: 30, carbs: 3, fat: 2, completed: false }
      ]
    },
    Tuesday: {
      workout: [
        { name: '5 x 1K intervals (Zone 3)', duration: '~40min', completed: false },
        { name: 'Stretch and mobility work', duration: '15min', completed: false }
      ],
      meals: [
        { time: '8 AM', name: 'Greek yogurt with berries + protein + toast', calories: 450, protein: 30, carbs: 45, fat: 12, completed: false },
        { time: '10 AM', name: '2 boiled eggs', calories: 140, protein: 12, carbs: 0, fat: 10, completed: false },
        { time: '12:30 PM', name: 'Grilled chicken breast with quinoa & spinach', calories: 420, protein: 35, carbs: 40, fat: 8, completed: false },
        { time: '3 PM', name: 'Chicken sausage with mustard', calories: 180, protein: 15, carbs: 2, fat: 12, completed: false },
        { time: '6 PM', name: 'Baked salmon with asparagus & sweet potato', calories: 450, protein: 40, carbs: 30, fat: 15, completed: false }
      ]
    },
    Wednesday: {
      workout: [
        { name: 'Dumbbell Shoulder Press', sets: 4, reps: 10, completed: false },
        { name: 'Bulgarian Split Squats', sets: 4, reps: '10 each leg', completed: false },
        { name: 'Pull-Ups', sets: 4, reps: 8, completed: false },
        { name: 'Deadlifts with Dumbbells', sets: 4, reps: 10, completed: false },
        { name: 'Hanging Leg Raise', sets: 4, reps: 15, completed: false }
      ],
      meals: [
        { time: '8 AM', name: 'Greek yogurt with berries + protein + toast', calories: 450, protein: 30, carbs: 45, fat: 12, completed: false },
        { time: '10 AM', name: '2 boiled eggs', calories: 140, protein: 12, carbs: 0, fat: 10, completed: false },
        { time: '12:30 PM', name: 'Grilled chicken breast with quinoa & spinach', calories: 420, protein: 35, carbs: 40, fat: 8, completed: false },
        { time: '3 PM', name: 'Chicken sausage with mustard', calories: 180, protein: 15, carbs: 2, fat: 12, completed: false },
        { time: '6 PM', name: 'Baked salmon with asparagus & sweet potato', calories: 450, protein: 40, carbs: 30, fat: 15, completed: false },
        { time: 'Post-Workout', name: 'Protein shake + creatine', calories: 150, protein: 30, carbs: 3, fat: 2, completed: false }
      ]
    }
  });

  // Demo mode - automatically show dashboard after component loads
  useState(() => {
    // For demo purposes only
    if (currentScreen === 'onboarding') {
      setTimeout(() => {
        setUserName('Alex');
        setEventName('Triathlon');
        setEventDate('2025-07-01');
        setCurrentScreen('dashboard');
      }, 1000);
    }
  }, []);

  // Phase descriptions
  const phaseDescriptions = {
    1: "Foundation & Conditioning",
    2: "Building Strength & Endurance",
    3: "Event-Specific Training & Peak Conditioning"
  };
  
  const phaseDetails = {
    1: "Focus on building basic strength and endurance. Workouts are designed to establish a foundation for more intense training in later phases.",
    2: "Increase volume and intensity to build more strength and stamina. Incorporate more sport-specific training elements.",
    3: "Peak conditioning phase with event simulation workouts. Highest volume and intensity to prepare you for event day."
  };
  
  // Handle onboarding submission
  const handleOnboardingSubmit = () => {
    if (userName && eventName && eventDate) {
      setShowNutritionSetup(true);
    }
  };
  
  // Handle nutrition setup submission
  const handleNutritionSetupSubmit = () => {
    setNutritionTargets({...nutritionSetupData});
    setDaysLeft(42); // Demo days left
    setCurrentScreen('dashboard');
    setShowNutritionSetup(false);
  };
  
  // Start editing an item
  const startEditing = (itemType, index) => {
    const item = getCurrentDayData()[itemType][index];
    setEditMode(true);
    setEditingItemType(itemType);
    setEditingItemIndex(index);
    setEditFormData({...item});
    setIsNewItem(false);
  };
  
  // Add a new custom item
  const addNewItem = (itemType) => {
    setEditMode(true);
    setEditingItemType(itemType);
    setIsNewItem(true);
    
    if (itemType === 'workout') {
      setEditFormData({
        name: '',
        sets: 3,
        reps: 10,
        completed: false,
        isCustom: true
      });
    } else {
      setEditFormData({
        name: '',
        time: '',
        calories: 0,
        protein: 0,
        carbs: 0,
        fat: 0,
        completed: false,
        isCustom: true
      });
    }
  };
  
  // Cancel editing
  const cancelEditing = () => {
    setEditMode(false);
    setEditingItemType(null);
    setEditingItemIndex(null);
    setEditFormData({});
    setIsNewItem(false);
  };
  
  // Save edited item
  const saveEditedItem = () => {
    const updatedTrainingData = {...trainingData};
    
    // Check if any required fields are empty
    if (!editFormData.name) {
      alert("Please fill in all required fields");
      return;
    }
    
    // Adding a new item
    if (isNewItem) {
      if (!updatedTrainingData[currentDay]) {
        updatedTrainingData[currentDay] = { workout: [], meals: [] };
      }
      
      if (editingItemType === 'workout') {
        updatedTrainingData[currentDay].workout.push({...editFormData});
      } else if (editingItemType === 'meal') {
        updatedTrainingData[currentDay].meals.push({...editFormData});
      }
    } 
    // Updating existing item
    else {
      if (editingItemType === 'workout') {
        updatedTrainingData[currentDay].workout[editingItemIndex] = {
          ...editFormData,
          completed: trainingData[currentDay].workout[editingItemIndex].completed
        };
      } else if (editingItemType === 'meal') {
        updatedTrainingData[currentDay].meals[editingItemIndex] = {
          ...editFormData,
          completed: trainingData[currentDay].meals[editingItemIndex].completed
        };
      }
    }
    
    setTrainingData(updatedTrainingData);
    cancelEditing();
  };
  
  // Handle input changes in edit form
  const handleEditFormChange = (e) => {
    const { name, value } = e.target;
    let parsedValue = value;
    
    // Convert numeric inputs to numbers
    if (name === 'sets' || name === 'reps' || name === 'calories' || 
        name === 'protein' || name === 'carbs' || name === 'fat') {
      parsedValue = isNaN(parseInt(value)) ? 0 : parseInt(value);
    }
    
    setEditFormData({
      ...editFormData,
      [name]: parsedValue
    });
  };
  
  // Handle nutrition setup changes
  const handleNutritionSetupChange = (e) => {
    const { name, value } = e.target;
    const parsedValue = isNaN(parseInt(value)) ? 0 : parseInt(value);
    
    setNutritionSetupData({
      ...nutritionSetupData,
      [name]: parsedValue
    });
  };
  
  // Toggle workout completion
  const toggleWorkoutCompletion = (index) => {
    const updatedTrainingData = {...trainingData};
    const currentWorkout = updatedTrainingData[currentDay].workout[index];
    currentWorkout.completed = !currentWorkout.completed;
    setTrainingData(updatedTrainingData);
  };
  
  // Handle meal completion toggle
  const toggleMealCompletion = (index) => {
    const updatedTrainingData = {...trainingData};
    const currentMeal = updatedTrainingData[currentDay].meals[index];
    currentMeal.completed = !currentMeal.completed;
    setTrainingData(updatedTrainingData);
  };

  // Handle day navigation
  const navigateDay = (direction) => {
    const days = Object.keys(trainingData);
    const currentIndex = days.indexOf(currentDay);
    let newIndex;
    
    if (direction === 'next') {
      newIndex = (currentIndex + 1) % days.length;
    } else {
      newIndex = (currentIndex - 1 + days.length) % days.length;
    }
    
    setCurrentDay(days[newIndex]);
  };
  
  // Get training data for the current day
  const getCurrentDayData = () => {
    return trainingData[currentDay] || {
      workout: [{ name: 'Rest day', completed: false }],
      meals: [{ time: '8 AM', name: 'Default meal', calories: 0, protein: 0, carbs: 0, fat: 0, completed: false }]
    };
  };
  
  // Calculate nutrition totals and percentages for the current day
  const calculateNutritionTotals = () => {
    const dayData = getCurrentDayData();
    const completedMeals = dayData.meals.filter(meal => meal.completed);
    
    const totals = {
      calories: completedMeals.reduce((sum, meal) => sum + (meal.calories || 0), 0),
      protein: completedMeals.reduce((sum, meal) => sum + (meal.protein || 0), 0),
      carbs: completedMeals.reduce((sum, meal) => sum + (meal.carbs || 0), 0),
      fat: completedMeals.reduce((sum, meal) => sum + (meal.fat || 0), 0)
    };
    
    const percentages = {
      calories: Math.min(Math.round((totals.calories / nutritionTargets.calories) * 100), 100),
      protein: Math.min(Math.round((totals.protein / nutritionTargets.protein) * 100), 100),
      carbs: Math.min(Math.round((totals.carbs / nutritionTargets.carbs) * 100), 100),
      fat: Math.min(Math.round((totals.fat / nutritionTargets.fat) * 100), 100)
    };
    
    return { totals, percentages };
  };
  
  // Render onboarding screen
  const renderOnboarding = () => (
    <div className="flex flex-col h-full bg-white">
      <div className="bg-blue-500 text-white p-4 text-center">
        <h1 className="text-2xl font-bold">TrainReady</h1>
      </div>
      
      <div className="flex-1 p-4 flex flex-col space-y-6">
        <div className="text-center mb-2">
          <h2 className="text-xl font-semibold">Let's Get Started!</h2>
          <p className="text-gray-600">Tell us about your training goal</p>
        </div>
        
        <div className="space-y-4">
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-1">Your Name</label>
            <input 
              className="w-full p-2 border border-gray-300 rounded-md"
              placeholder="Enter your name"
              value={userName}
              onChange={(e) => setUserName(e.target.value)}
            />
          </div>
          
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-1">Event Name</label>
            <input 
              className="w-full p-2 border border-gray-300 rounded-md"
              placeholder="What are you training for?"
              value={eventName}
              onChange={(e) => setEventName(e.target.value)}
            />
          </div>
          
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-1">Event Date</label>
            <input 
              className="w-full p-2 border border-gray-300 rounded-md"
              type="date"
              placeholder="When is your event?"
              value={eventDate}
              onChange={(e) => setEventDate(e.target.value)}
            />
          </div>
        </div>
        
        <div className="mt-auto">
          <button 
            className="w-full bg-blue-500 text-white py-3 rounded-md font-semibold flex items-center justify-center"
            onClick={handleOnboardingSubmit}
          >
            Next <ArrowRight className="ml-2" size={18} />
          </button>
        </div>
      </div>
    </div>
  );
  
  // Render nutrition setup screen
  const renderNutritionSetup = () => (
    <div className="absolute inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-10">
      <div className="bg-white rounded-lg p-4 max-w-md w-full">
        <div className="flex justify-between items-center mb-4">
          <h3 className="font-bold text-xl">Set Your Nutrition Targets</h3>
        </div>
        
        <p className="text-gray-600 mb-4">
          Set your daily nutrition goals to track your progress throughout training.
        </p>
        
        <div className="space-y-4 mb-6">
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-1">Daily Calories</label>
            <input 
              className="w-full p-2 border border-gray-300 rounded-md"
              name="calories"
              type="number"
              value={nutritionSetupData.calories}
              onChange={handleNutritionSetupChange}
            />
          </div>
          
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-1">Protein (g)</label>
            <input 
              className="w-full p-2 border border-gray-300 rounded-md"
              name="protein"
              type="number"
              value={nutritionSetupData.protein}
              onChange={handleNutritionSetupChange}
            />
          </div>
          
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-1">Carbs (g)</label>
            <input 
              className="w-full p-2 border border-gray-300 rounded-md"
              name="carbs"
              type="number"
              value={nutritionSetupData.carbs}
              onChange={handleNutritionSetupChange}
            />
          </div>
          
          <div>
            <label className="block text-sm font-medium text-gray-700 mb-1">Fat (g)</label>
            <input 
              className="w-full p-2 border border-gray-300 rounded-md"
              name="fat"
              type="number"
              value={nutritionSetupData.fat}
              onChange={handleNutritionSetupChange}
            />
          </div>
        </div>
        
        <button 
          className="w-full bg-blue-500 text-white py-3 rounded-md font-semibold flex items-center justify-center"
          onClick={handleNutritionSetupSubmit}
        >
          Create My Plan <ArrowRight className="ml-2" size={18} />
        </button>
      </div>
    </div>
  );
  
  // Render edit form for workout or meal
  const renderEditForm = () => {
    const itemType = editingItemType;
    const formTitle = isNewItem ? `Add Custom ${itemType === 'workout' ? 'Workout' : 'Meal'}` : 
                                 `Edit ${itemType === 'workout' ? 'Workout' : 'Meal'}`;
    
    return (
      <div className="absolute inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-10">
        <div className="bg-white rounded-lg p-4 max-w-sm w-full">
          <div className="flex justify-between items-center mb-4">
            <h3 className="font-bold text-lg">{formTitle}</h3>
            <button 
              className="text-gray-500"
              onClick={cancelEditing}
            >
              <X size={20} />
            </button>
          </div>
          
          <div className="space-y-4">
            {itemType === 'workout' && (
              <>
                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-1">Workout Name</label>
                  <input 
                    className="w-full p-2 border border-gray-300 rounded-md"
                    name="name"
                    value={editFormData.name || ''}
                    onChange={handleEditFormChange}
                    placeholder="Enter workout name"
                  />
                </div>
                
                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-1">Sets</label>
                  <input 
                    className="w-full p-2 border border-gray-300 rounded-md"
                    name="sets"
                    type="number"
                    min="1"
                    value={editFormData.sets || ''}
                    onChange={handleEditFormChange}
                    placeholder="Number of sets"
                  />
                </div>
                
                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-1">Reps</label>
                  <input 
                    className="w-full p-2 border border-gray-300 rounded-md"
                    name="reps"
                    value={editFormData.reps || ''}
                    onChange={handleEditFormChange}
                    placeholder="Number of reps or duration"
                  />
                </div>
                
                {/* Duration field optional for workouts that need it */}
                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-1">Duration (optional)</label>
                  <input 
                    className="w-full p-2 border border-gray-300 rounded-md"
                    name="duration"
                    value={editFormData.duration || ''}
                    onChange={handleEditFormChange}
                    placeholder="e.g. 30 min, 45 sec"
                  />
                </div>
              </>
            )}
            
            {itemType === 'meal' && (
              <>
                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-1">Meal</label>
                  <input 
                    className="w-full p-2 border border-gray-300 rounded-md"
                    name="name"
                    value={editFormData.name || ''}
                    onChange={handleEditFormChange}
                    placeholder="Enter meal description"
                  />
                </div>
                
                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-1">Time</label>
                  <input 
                    className="w-full p-2 border border-gray-300 rounded-md"
                    name="time"
                    value={editFormData.time || ''}
                    onChange={handleEditFormChange}
                    placeholder="e.g. 8 AM, 12:30 PM"
                  />
                </div>
                
                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-1">Calories</label>
                  <input 
                    className="w-full p-2 border border-gray-300 rounded-md"
                    name="calories"
                    type="number"
                    min="0"
                    value={editFormData.calories || 0}
                    onChange={handleEditFormChange}
                    placeholder="Calories"
                  />
                </div>
                
                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-1">Protein (g)</label>
                  <input 
                    className="w-full p-2 border border-gray-300 rounded-md"
                    name="protein"
                    type="number"
                    min="0"
                    value={editFormData.protein || 0}
                    onChange={handleEditFormChange}
                    placeholder="Protein in grams"
                  />
                </div>
                
                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-1">Carbs (g)</label>
                  <input 
                    className="w-full p-2 border border-gray-300 rounded-md"
                    name="carbs"
                    type="number"
                    min="0"
                    value={editFormData.carbs || 0}
                    onChange={handleEditFormChange}
                    placeholder="Carbs in grams"
                  />
                </div>
                
                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-1">Fat (g)</label>
                  <input 
                    className="w-full p-2 border border-gray-300 rounded-md"
                    name="fat"
                    type="number"
                    min="0"
                    value={editFormData.fat || 0}
                    onChange={handleEditFormChange}
                    placeholder="Fat in grams"
                  />
                </div>
              </>
            )}
          </div>
          
          <div className="mt-6 flex space-x-2">
            <button 
              className="flex-1 bg-gray-200 py-2 rounded font-medium"
              onClick={cancelEditing}
            >
              Cancel
            </button>
            <button 
              className="flex-1 bg-blue-500 text-white py-2 rounded font-medium flex items-center justify-center"
              onClick={saveEditedItem}
            >
              <Save size={16} className="mr-1" />
              Save
            </button>
          </div>
        </div>
      </div>
    );
  };
  
  // Render dashboard screen
  const renderDashboard = () => {
    const dayData = getCurrentDayData();
    
    if (!dayData) {
      return (
        <div className="flex flex-col h-full items-center justify-center">
          <AlertCircle size={48} className="text-orange-500 mb-4" />
          <p className="text-gray-700">Training plan is being prepared...</p>
        </div>
      );
    }
    
    const dayWorkouts = dayData.workout;
    const dayMeals = dayData.meals;
    
    const workoutCompletionRate = dayWorkouts.filter(w => w.completed).length / dayWorkouts.length;
    const mealCompletionRate = dayMeals.filter(m => m.completed).length / dayMeals.length;
    
    const { totals, percentages } = calculateNutritionTotals();
    
    return (
      <div className="flex flex-col h-full bg-white">
        {/* Header */}
        <div className="bg-blue-500 text-white p-4">
          <div className="flex justify-between items-center mb-2">
            <h1 className="text-xl font-bold">TrainReady</h1>
            <div className="flex items-center">
              <Calendar size={16} className="mr-1" />
              <span className="text-sm">{daysLeft} days until {eventName}</span>
            </div>
          </div>
          
          <div className="flex items-center justify-between">
            <div className="flex items-center">
              <User size={16} className="mr-1" />
              <span>Hi, {userName}!</span>
            </div>
            <button 
              className="bg-blue-700 rounded-full px-3 py-1 text-xs font-medium flex items-center"
              onClick={() => setShowPhaseInfo(!showPhaseInfo)}
            >
              <Award size={14} className="mr-1" />
              Phase {currentPhase}: {phaseDescriptions[currentPhase]}
            </button>
          </div>
        </div>
        
        {/* Phase Info Modal */}
        {showPhaseInfo && (
          <div className="absolute inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-10">
            <div className="bg-white rounded-lg p-4 max-w-sm w-full">
              <div className="flex justify-between items-center mb-4">
                <h3 className="font-bold text-lg">Phase {currentPhase}</h3>
                <button 
                  className="text-gray-500"
                  onClick={() => setShowPhaseInfo(false)}
                >
                  <X size={20} />
                </button>
              </div>
              
              <h4 className="font-semibold text-blue-600 mb-2">{phaseDescriptions[currentPhase]}</h4>
              <p className="text-gray-700 mb-4">{phaseDetails[currentPhase]}</p>
              
              <div className="grid grid-cols-3 gap-2 mb-4">
                <div className={`text-center p-2 rounded ${currentPhase === 1 ? 'bg-blue-500 text-white' : 'bg-gray-100'}`}>
                  <div className="font-bold">Phase 1</div>
                  <div className="text-xs">Foundation</div>
                </div>
                <div className={`text-center p-2 rounded ${currentPhase === 2 ? 'bg-blue-500 text-white' : 'bg-gray-100'}`}>
                  <div className="font-bold">Phase 2</div>
                  <div className="text-xs">Building</div>
                </div>
                <div className={`text-center p-2 rounded ${currentPhase === 3 ? 'bg-blue-500 text-white' : 'bg-gray-100'}`}>
                  <div className="font-bold">Phase 3</div>
