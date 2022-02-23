<template>
    <div
        class="fixed z-10 inset-0 overflow-y-auto transition-all"
        aria-labelledby="modal-title"
        role="dialog"
        aria-modal="true"
    >
        <div class="flex pt-4 px-4 pb-20 text-center sm:block sm:p-0">
            <div
                class="fixed inset-0 bg-gray-400 bg-opacity-90 transition-opacity"
                aria-hidden="true"
            ></div>
            <div
                class="inline-block align-bottom pt-5 pb-4 overflow-hidden transform transition-all sm:my-8 sm:align-middle sm:w-full sm:p-6"
            >
                <div>
                    <div class="text-center mt-5">
                        <slot />
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>